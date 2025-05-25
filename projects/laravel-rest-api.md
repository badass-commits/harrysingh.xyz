---
layout: project
title: laravel-rest-api
date: 2022-02-24 15:22:42 -0600
category: projects
---


# Building a RESTful API with Laravel 5.8

I recently created a simple RESTful API using Laravel 5.8, focusing on core features like user authentication and CRUD operations for posts and comments. The goal was to set up a clean and minimal backend that could serve as a starting point for future projects.

## Features

- User registration and login with token-based authentication
- CRUD operations for posts and comments
- Use of Laravel API Resources for consistent JSON responses
- Protected routes for authenticated users

## Getting Started

To get the project up and running:

1. Clone the repository:

   ```bash
   git clone https://github.com/badass-commits/laravel-rest-api.git
   cd laravel-rest-api
   ```

2. Install dependencies:

   ```bash
   composer install
   ```

3. Copy the example environment file and generate an application key:

   ```bash
   cp .env.example .env
   php artisan key:generate
   ```

4. Configure your database settings in the `.env` file.

5. Run migrations:

   ```bash
   php artisan migrate
   ```

6. Start the development server:

   ```bash
   php artisan serve
   ```

## API Endpoints

- `POST /api/register` – Register a new user
- `POST /api/login` – Authenticate a user and receive a token
- `GET /api/posts` – Retrieve all posts
- `POST /api/posts` – Create a new post
- `GET /api/posts/{id}` – Retrieve a specific post
- `PUT /api/posts/{id}` – Update a post
- `DELETE /api/posts/{id}` – Delete a post

All routes under `/api/posts` are protected and require authentication via a Bearer token.

## Conclusion

This project serves as a foundational template for building RESTful APIs with Laravel 5.8. It's straightforward and easy to extend, making it suitable for small to medium-sized applications.

Feel free to check out the repository: [laravel-rest-api](https://github.com/badass-commits/laravel-rest-api)
