---
layout: project
title: react-laravel-jwt-auth
date: 2024-01-27 14:53:12 -0600
category: projects
---


# Building a Full-Stack JWT Auth App with Laravel and React

I recently put together a boilerplate for full-stack JWT authentication using Laravel for the backend and React for the frontend. It's designed to provide a clean starting point for projects that need secure user authentication.

## What's Inside

### Laravel Backend
- Laravel Framework: Handles API endpoints and business logic.
- Tymon JWT Package: Implements JWT-based API authentication.
- MySQL Database: Structured to support user authentication workflows.

### React Frontend
- React JS: Builds the user interface.
- React Router: Manages navigation and routing.
- Bootstrap: Provides styling and responsive design.

## Getting Started

1. Clone the Repository:

   ```bash
   git clone https://github.com/badass-commits/react-laravel-jwt-auth.git
   cd react-laravel-jwt-auth
   ```

2. Set Up the Backend:
   - Navigate to the `backend` directory.
   - Install dependencies:

     ```bash
     composer install
     ```

   - Configure your `.env` file with database credentials.
   - Run migrations:

     ```bash
     php artisan migrate
     ```

   - Generate JWT secret:

     ```bash
     php artisan jwt:secret
     ```

   - Start the server:

     ```bash
     php artisan serve
     ```

3. Set Up the Frontend:
   - Navigate to the `frontend` directory.
   - Install dependencies:

     ```bash
     npm install
     ```

   - Start the development server:

     ```bash
     npm start
     ```

## Repository

Feel free to explore the project here: [react-laravel-jwt-auth](https://github.com/badass-commits/react-laravel-jwt-auth)
