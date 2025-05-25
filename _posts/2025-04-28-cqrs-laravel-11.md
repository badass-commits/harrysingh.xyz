---
layout: post
title: "CQRS with Laravel 11"
date: 2025-04-28 14:00:00 -0600
---

As business logic becomes more complex, services can become bloated, classes may do too much, and tests become hard to maintain. To address these issues, the author applied the CQRS (Command Query Responsibility Segregation) pattern in Laravel projects, leading to improved code clarity and maintainability.

## What is CQRS?

CQRS is an architectural pattern that separates commands (operations that change the system’s state) from queries (operations that read data). This separation:

- Reflects business intent more clearly in code
- Makes unit testing easier
- Keeps classes small and focused
- Can improve performance by optimizing read and write paths separately

In practice, this involves creating separate classes for each action, typically organized under `Commands/` and `Queries/`, each with its own handler.

## Setting up CQRS in Laravel

To maintain organization, commands and queries are placed under a `CQRS` folder:

```
app/
├── CQRS/
│   ├── Commands/
│   │   ├── GenerateMonthlyInvoiceCommand.php
│   │   └── GenerateMonthlyInvoiceHandler.php
│   └── Queries/
│       ├── GetInvoiceBreakdownQuery.php
│       └── GetInvoiceBreakdownHandler.php
```

This structure makes it easy to reason about the application’s use cases.

## Implementing a Simple Command Bus

A command bus is used to automatically find the right handler for any command or query based on a naming convention (`Command` ➔ `CommandHandler`, `Query` ➔ `QueryHandler`). Here's a simplified version:

```php
namespace App\Services;

use Illuminate\Pipeline\Pipeline;

class CommandBus
{
    public function __construct(
        protected array $middlewares = []
    ) {}

    public function dispatch(object $command): mixed
    {
        $handler = $this->resolveHandler($command);

        return app(Pipeline::class)
            ->send($command)
            ->through($this->middlewares)
            ->then(fn ($command) => $handler->handle($command));
    }

    protected function resolveHandler(object $command): object
    {
        $handlerClass = get_class($command) . 'Handler';

        if (!class_exists($handlerClass)) {
            throw new \RuntimeException("Handler [{$handlerClass}] not found for command " . get_class($command));
        }

        return app($handlerClass);
    }
}
```

Middlewares, such as logging or validation, can be added around the execution:

```php
namespace App\Services\Middlewares;

use Closure;

class LogCommandExecution
{
    public function handle(object $command, Closure $next)
    {
        logger()->info('Executing command: ' . get_class($command));

        return $next($command);
    }
}
```

Register the command bus in your service provider:

```php
use App\Services\CommandBus;

public function register()
{
    $this->app->singleton(CommandBus::class, function () {
        return new CommandBus([
            \App\Services\Middlewares\LogCommandExecution::class,
        ]);
    });
}
```

## Common Structure

- **Writes:**
  - `Command`: Holds the input data
  - `CommandHandler`: Contains the business logic

- **Reads:**
  - `Query`: Describes the data you want
  - `QueryHandler`: Handles the logic and returns a DTO or array

## Naming Commands and Queries

Class names should reflect business intent:

- Prefer: `GenerateMonthlyInvoiceCommand`, `AssignRoleToUserCommand`, `GetInvoiceBreakdownQuery`
- Avoid: Generic names like `InvoiceService`, `Handler`, `DoStuff`

This approach makes it easier for non-technical stakeholders to understand what a command does.

## When to Use CQRS

CQRS is beneficial when:

- You have rich business rules (state checks, validations, calculations)
- You need to aggregate data before writing
- You want to structure your code around business use cases
- You're building modular or DDD-style architectures

For simple CRUD operations, CQRS might be overkill.

## Real-World Example: Generating a Monthly Invoice

### Context:

At the end of each month, the system must generate an invoice for a customer based on multiple data sources (subscriptions, one-time services, product usage). Before saving the invoice, it needs to:

- Retrieve all usage records for the month
- Calculate the subtotal, taxes, and possible discounts
- Build invoice line items
- Save everything to the database

### Command:

```php
class GenerateMonthlyInvoiceCommand
{
    public function __construct(
        public readonly int $customerId,
        public readonly DateTimeInterface $month
    ) {}
}
```

### Handler:

```php
class GenerateMonthlyInvoiceHandler
{
    public function __construct(
        private ConsumptionRepository $consumptions,
        private InvoiceRepository $invoices,
        private TaxService $taxService,
        private DiscountService $discountService,
    ) {}

    public function handle(GenerateMonthlyInvoiceCommand $command): void
    {
        $items = $this->consumptions->forCustomerAndMonth($command->customerId, $command->month);

        if ($items->isEmpty()) {
            throw new DomainException('No usage to invoice.');
        }

        $subtotal = $items->sum(fn($item) => $item->price);
        $taxes = $this->taxService->compute($command->customerId, $subtotal);
        $discount = $this->discountService->apply($command->customerId, $items);
        $total = $subtotal + $taxes - $discount;

        $invoice = new Invoice(
            customerId: $command->customerId,
            month: $command->month,
            subtotal: $subtotal,
            taxes: $taxes,
            discount: $discount,
            total: $total
        );

        $invoice->addLinesFromConsumption($items);
        $this->invoices->save($invoice);
    }
}
```

### Query:

```php
class GetInvoiceBreakdownQuery
{
    public function __construct(
        public readonly int $customerId,
        public readonly DateTimeInterface $month
    ) {}
}
```

### Handler:

```php
class GetInvoiceBreakdownHandler
{
    public function __construct(private InvoiceRepository $invoices) {}

    public function handle(GetInvoiceBreakdownQuery $query): InvoiceDTO
    {
        $invoice = $this->invoices->findByCustomerAndMonth($query->customerId, $query->month);
        return new InvoiceDTO($invoice);
    }
}
```

## Benefits Observed

- **Clarity:** Command and query names clearly describe business actions
- **Isolation:** Each handler is easy to test independently
- **Organization:** Fits perfectly in a modular architecture
- **Scalability:** Easily plug in validation, logging, or events without bloating controllers

## Testing Handlers

CQRS simplifies unit testing. Each command or query is an isolated unit that can be tested without going through a controller or infrastructure.

### Example Test:

```php
test('it generates an invoice with correct totals') {
    $consumptions = collect([
        new ConsumptionItem(price: 100),
        new ConsumptionItem(price: 200),
    ]);

    $handler = new GenerateMonthlyInvoiceHandler(
        new InMemoryConsumptionRepository($consumptions),
        new FakeInvoiceRepository(),
        new FixedTaxService(20),
        new FixedDiscountService(30)
    );

    $handler->handle(new GenerateMonthlyInvoiceCommand(1, now()));

    expect(FakeInvoiceRepository::$savedInvoice)->not->toBeNull();
    expect(FakeInvoiceRepository::$savedInvoice->total)->toBe(290); // 300 + 20 - 30
}
```

## Conclusion

CQRS is a valuable tool for structuring code when business logic becomes complex. It makes intentions explicit, responsibilities more focused, and code easier to test. While not necessary for every situation, it's beneficial when services start feeling heavy or messy.

## Bonus: CQRS vs CQS

- **CQS (Command Query Separation):** A design principle where a method should either modify state (command) or return data (query), but never both.
- **CQRS (Command Query Responsibility Segregation):** Applies this principle at the application level by separating models, services, and logic for reads and writes.

In essence, CQRS is structural, while CQS is behavioral.
