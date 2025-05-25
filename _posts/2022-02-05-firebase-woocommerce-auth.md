---
layout: post
title: "Firebase WooCommerce Auth – WordPress Plugin"
date: 2022-04-12 15:00:00 -0600
---

I recently built a WordPress plugin that lets you log into a WooCommerce store using Firebase Authentication. It’s called **Firebase WooCommerce Auth**, and it supports Google, GitHub, Microsoft, phone sign-in, email/password, and even email magic links.

The plugin connects Firebase Auth with WooCommerce in a secure, seamless way. It dynamically creates WordPress user accounts on login, syncs profile data like email and phone, and integrates directly into WooCommerce's session system so users stay logged in through the checkout process.

## Why I Built It

Many store owners want a simple, secure, and modern way to let users sign in—especially from mobile. Firebase does a great job of handling auth securely and scalably, but bridging that into WordPress (especially WooCommerce) wasn’t straightforward. This plugin fixes that.

## Key Features

- 🔐 Secure login via Firebase Authentication
- 🛒 WooCommerce session integration + billing field population
- 🧩 Supports Google, Phone, GitHub, Twitter, Microsoft, and more
- ⚙️ Admin settings page for Firebase config
- 💬 Customizable legal links (TOS, privacy policy)
- 🧑 Prompt for email if missing (e.g., from phone-only sign-in)

## Example UI

Here's what the admin side looks like:

This is the Firebase configuration screen where the site admin pastes in keys from the Firebase project. It ensures secure communication between the WordPress plugin and Firebase.
<p align="center">
  <img src="/assets/images/posts/Firebase%20Configuration.png" alt="Firebase Config" width="70%" />
</p>

This shows the sign-in methods you can enable—like Google, GitHub, Phone, or Email. These toggle switches make it easy to control what your users see.
<p align="center">
  <img src="/assets/images/posts/Sign-In%20Methods.png" alt="Auth Providers" width="70%" />
</p>

Here’s how the plugin integrates seamlessly into the WooCommerce checkout flow, giving users a smooth login experience before they complete a purchase.
<p align="center">
  <img src="/assets/images/posts/Easy%20login%20during%20the%20checkout.png" alt="Legal Links Settings" width="70%" />
</p>

## Shortcode Usage

Place this shortcode on any login or signup page:

```html
[firebase_auth_ui]
```

It will render FirebaseUI, allowing users to sign in using the enabled methods.

## Reflections & What’s Next

Building this plugin taught me how to bridge modern authentication flows with legacy platforms like WordPress and WooCommerce. I gained experience working with the Firebase JS SDK, handling async auth flows, and syncing third-party profiles with native user objects.

If I had more time, I’d love to add more fine-grained control over user roles on signup, improve styling flexibility for the auth widget, and add analytics hooks to better understand how users log in.
