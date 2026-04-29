# Inkwell

Inkwell is a NestJS backend for managing books, borrowing activity, and user accounts. The project combines authentication, role-based access control, email-based account flows, and a MySQL database layer in a modular service structure.

## Overview

This API is organized around four core areas:

- book management
- borrowing and return tracking
- user authentication and account management
- email verification and password reset flows

The codebase uses NestJS modules to keep these responsibilities separated and easier to extend.

## Tech Stack

- NestJS
- TypeORM
- MySQL
- JWT authentication
- Nodemailer
- class-validator
- class-transformer

## Project Structure

```text
src/
  app.controller.ts
  app.module.ts
  app.service.ts
  main.ts
  books/
  borrow/
  mailer/
  seeder/
  user/
  utils/
```

## Repository

```bash
git clone https://github.com/blessed-winner/Inkwell.git
cd nest-books
```

## Getting Started

### 1. Install dependencies

```bash
npm install
```

### 2. Configure environment variables

Create a `.env` file in the project root and provide values such as:

```env
DB_HOST=localhost
DB_PORT=3306
DB_USERNAME=root
DB_PASSWORD=your_password
DB_NAME=books_auth
PORT=3000
JWT_SECRET=your_jwt_secret
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=your_smtp_username
SMTP_PASS=your_smtp_password
SMTP_SECURE=false
MAIL_FROM="Inkwell <noreply@inkwell.com>"
```

### 3. Start the development server

```bash
npm run start:dev
```

## Available Scripts

```bash
npm run build
npm run start
npm run start:dev
npm run start:debug
npm run start:prod
npm run lint
npm run format
npm run test
npm run test:e2e
```

## Core Modules

### `books`

Handles creating, listing, updating, deleting, and viewing book borrowing history.

### `borrow`

Handles borrowing a book and marking it as returned.

### `user`

Handles signup, login, account verification, password reset, user creation, and borrowing history lookup.

### `mailer`

Handles email delivery for verification and password reset workflows.

## API Summary

### Authentication and users

- `POST /auth/signup`
- `GET /auth/verify-email`
- `POST /auth/login`
- `POST /auth/create`
- `PATCH /auth/profile`
- `POST /auth/request-reset`
- `POST /auth/reset-password`
- `GET /auth/:id/history`

### Books

- `POST /books`
- `GET /books`
- `GET /books/:id`
- `PATCH /books/:id`
- `DELETE /books/:id`
- `GET /books/:id/history`

### Borrowing

- `POST /borrow`
- `PATCH /borrow/:id`

## Roles and Access

The application defines three roles:

- `user`
- `librarian`
- `admin`

Book creation and updates are restricted to elevated roles, while deletion is limited to administrators. JWT-based guards protect authenticated routes.

## Data Model

### User

- `id`
- `name`
- `email`
- `password`
- `role`
- `isVerified`
- `resetToken`
- `resetTokenExpiry`

### Book

- `id`
- `title`
- `author`

### Borrow

- `id`
- `book`
- `user`
- `borrowedAt`
- `returnedAt`

## Notes

- Configuration is loaded through `@nestjs/config`.
- Database connection settings are read from `.env`.
- TypeORM is configured with `synchronize: true`, which is convenient for development but should be reviewed before production use.

## License

This project is currently marked as `UNLICENSED` in `package.json`.
