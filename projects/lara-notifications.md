---
layout: project
title: lara-notifications
date: 2022-02-24 15:22:42 -0600
category: projects
---

# Creating a Simple Notification System in Laravel

Every once in a while, I build something small that ends up being surprisingly useful across multiple projects. This time, it was a lightweight notification system for Laravel. Nothing fancy — just something that lets me store and display notifications in a clean, flexible way.

I called it [lara-notifications](https://github.com/badass-commits/lara-notifications), and it's now a reusable package I can pull into any Laravel project when I need basic app-level notifications.

## Why this, when Laravel already has notifications?

Laravel’s built-in notification system is pretty robust. It supports mail, Slack, database, broadcast, and more. But for some projects, I just wanted something simpler — no queues, no channels — just persistent, in-app notifications I could show in the UI.

Think of it like the notifications you see in admin dashboards or CMS tools:  
“New user signed up.”  
“Payment failed.”  
“Someone left a comment.”

That kind of stuff.

## What it does

The package provides a simple `Notification` model with fields like title, body, type (info, success, error, etc.), and whether it’s been read. There’s a basic CRUD interface for creating and managing them, and I also included a component for rendering them in a Blade view.

Right now, the features are pretty minimal on purpose:

- Add and delete notifications
- Mark as read/unread
- Optional expiration
- Simple styling out of the box

I wanted it to feel lightweight and drop-in ready, without pulling in extra dependencies.

## How I built it

This started as a one-off class I wrote for a dashboard project, but it made sense to turn it into a small package. Laravel makes this process pretty painless — I used `artisan make:package` to scaffold things and just built on top of the default structure.

There’s no custom frontend JS here — it’s all server-rendered Blade, which I actually prefer for stuff like this. It’s easy to slot into existing layouts and works with whatever framework or component system I’m already using.

## Lessons learned

One of the things I realized working on this is how helpful it is to keep your utilities composable. Instead of trying to make this notification system handle everything, I kept it focused on just the UI layer. If I need emails or real-time events, I can still use Laravel’s built-in features.

Also, turning something from a one-off into a package made me think more about API design, config defaults, and usability for other developers (even if that developer is just “future me”).

## Plans for the future

Right now it does what I need, but I might add:

- A Livewire/Alpine.js component for auto-updating
- Support for user-specific notifications (currently it’s app-level)
- More styles/themes for different UI use cases
- Better integration with Laravel policies and middleware

If any of that sounds useful to you, feel free to contribute or fork it.

## Try it out

If you're working on a Laravel app and need a dead-simple way to show persistent notifications to users (without dragging in extra complexity), give it a look:

[https://github.com/badass-commits/lara-notifications](https://github.com/badass-commits/lara-notifications)

I’ll probably keep tweaking it here and there as I use it in more projects.

If you end up trying it out or extending it, I’d be curious to see how you're using it.
