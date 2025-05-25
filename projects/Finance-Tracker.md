---
layout: project
title: Finance-Tracker
date: 2024-05-04 15:22:42 -0600
category: projects
---

# Building My Own Finance Tracker with ASP.NET MVC

For the longest time, I wasn’t really in control of my spending. I had a vague idea of where my money was going, but nothing concrete. I’d occasionally try a budgeting app, only to stop using it a week later. Most of them were either too complicated or just didn’t click with the way I think.

So I decided to build my own.

I called it [Finance Tracker](https://github.com/badass-commits/finance-tracker), and it’s a simple ASP.NET MVC web app that helps me track my income, expenses, and get a clearer picture of my financial habits.

## Why build something like this?

Honestly, it started as a side project just to sharpen my .NET skills. But pretty quickly, I realized I could actually use it in my day-to-day life. I didn’t want a full-blown accounting system or a flashy app with graphs everywhere. I just wanted something clean, minimal, and functional.

I also liked the idea of owning my data. No ads, no cloud syncing, no subscriptions. Just a private tool that lives on my own machine (or a server I control) and helps me stay on top of things.

## What it does

The app lets you:

- Create categories for transactions (like "Groceries", "Salary", "Subscriptions")
- Add income and expense entries with notes and timestamps
- View a simple dashboard that breaks down your finances
- Manage everything through a straightforward web interface

There’s basic authentication using ASP.NET Identity, so it supports multiple users if needed. But right now, I’m the only one using it.

## How it's built

It’s a standard ASP.NET MVC project. Views are Razor-based, and I’m using Entity Framework Core with SQL Server for the backend. Nothing too fancy — just a clean architecture and enough structure to make future features easy to add.

One thing I appreciated about sticking with MVC was the control over routing, view structure, and form handling. It felt a lot more straightforward than working within the constraints of a more “opinionated” front-end-heavy stack.

## What I learned

Even though it’s not a huge project, working on this taught me a lot. Mainly, how small improvements to tooling can have a real impact on daily habits. I also got more comfortable working with Identity and EF Core migrations, and was reminded that building software for yourself is one of the most rewarding kinds of development.

## What's next

Right now, I’m thinking about:

- Adding recurring transactions
- Generating monthly reports
- Exporting data to CSV
- Making the UI more responsive for mobile

Eventually, I might host it somewhere properly and secure it with HTTPS and 2FA. But for now, it’s just running locally — and that’s enough.

## Final thoughts

This isn’t meant to compete with apps like YNAB or Mint. It’s just a personal tool that solves a problem for me, in a way that’s simple and satisfying. If you’re curious about the code or want to adapt it for your own needs, feel free to check out the repo:

[https://github.com/badass-commits/finance-tracker](https://github.com/badass-commits/finance-tracker)

And if you’ve built something similar — or are thinking about it — I’d love to hear how you approached it.
