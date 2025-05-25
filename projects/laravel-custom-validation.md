---
layout: project
title: laravel-custom-validation
date: 2023-12-03 11:06:12 -0600
category: projects
---

# Enhancing Laravel Validation: Custom Rules for Real-World Needs

In many of my Laravel projects, I often encounter scenarios where the built-in validation rules don't quite meet the specific requirements of the application. Whether it's validating a national ID format, ensuring a mobile number has exactly 11 digits, or restricting file uploads to certain MIME types, these unique cases call for custom solutions.

To address these needs, I developed a set of custom validation rules tailored for Laravel applications. You can find the repository here:  
👉 [github.com/badass-commits/laravel-custom-validation](https://github.com/badass-commits/laravel-custom-validation)

## Why Custom Validation Rules?

Laravel's default validation rules are great, but sometimes you need more specific logic. For example:

- **National ID Validation**: Ensures a provided NID matches a given format or checksum.
- **Mobile Number Validation**: Checks that a number has exactly 11 digits, possibly with specific starting digits.
- **Floating-Point Validation**: Validates a float with precision or range constraints.
- **MIME Restrictions**: Accepts or rejects specific MIME types for uploads.

By creating custom rule classes, I can cleanly encapsulate this logic and reuse it wherever I need.

## What’s Included in the Package?

The repository currently includes:

- `FloatNumberCustomValidation`
- `MimeExclusion`
- `MimeInclusion`
- `MobileNumber11DigitCustomValidation`
- `NidSmartCardCustomValidation`

Each class implements Laravel’s validation rule interface, and can be used like any other validation rule in a controller or FormRequest.

## How to Use

Let’s say you want to validate that a mobile number is 11 digits long.

### Step 1 – Import the Rule

```
use App\Rules\MobileNumber11DigitCustomValidation;
```

### Step 2 – Apply in Validation

```
$request->validate([
    'mobile_number' => ['required', new MobileNumber11DigitCustomValidation()],
]);
```

## Getting Started

1.	Clone the repository:
```
git clone https://github.com/badass-commits/laravel-custom-validation.git
```
2.	Copy the rule classes you need into your Laravel app under app/Rules/.
3.	Use the rules in your validation logic as shown above.

## Final Thoughts
Custom validation rules might seem like a small thing, but they really help keep your logic clean and modular — especially in complex or domain-specific applications. If you find this useful or have ideas for additional rules, feel free to fork the repo or open a PR. Always happy to improve this for future use.