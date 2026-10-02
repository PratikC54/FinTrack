# FinTrack

FinTrack is a personal finance application built with React, Express,
PostgreSQL, and Prisma. It lets each user create accounts and categories,
record income and expenses, and view a monthly dashboard.

## What is included

- Secure registration and login with hashed passwords and JWT sessions.
- Per-user accounts with opening balances.
- Per-user income and expense categories.
- Create, edit, and delete transactions. Account balances update with each transaction.
- Dashboard with total balance, this month's income/expenses, category spending, accounts, and recent transactions.
- Protected API routes: one user cannot access another user's data.

## Project layout

```
fintrack-ui/       React and Vite frontend
fintrack-node/     Express API and Prisma schema
  prisma/          PostgreSQL data model and migrations
  src/config/      environment and Prisma configuration
  src/controllers/ request-handling code
  src/middleware/  authentication and error handling
  src/routes/      API URL definitions
```

## First-time setup

PostgreSQL is installed on this computer, but you need to supply the password chosen for its `postgres` user. The sample `.env` file has a placeholder and will not connect until it is changed.

1. Create a database named `fintrack` in pgAdmin's Query Tool:

   ```sql
   CREATE DATABASE fintrack;
   ```

2. Open `fintrack-node/.env` and update `DATABASE_URL` with your real PostgreSQL password. Also replace `JWT_SECRET` with a long random value.

3. Create the tables from the Prisma schema:

   ```powershell
   cd D:\Fintrack\fintrack-node
   npm run prisma:migrate -- --name init
   ```

4. Start the API in one terminal:

   ```powershell
   cd D:\Fintrack\fintrack-node
   npm run dev
   ```

5. Start the React app in another terminal:

   ```powershell
   cd D:\Fintrack\fintrack-ui
   npm run dev
   ```

6. Open the Vite URL shown in the terminal, normally `http://localhost:5173`.

If your terminal has the earlier npm path problem, run the system npm directly:

```powershell
& 'C:\Program Files\nodejs\npm.cmd' run dev
```

## API endpoints

| Area | Endpoint |
| --- | --- |
| Health check | `GET /api/health` |
| Authentication | `POST /api/auth/register`, `POST /api/auth/login`, `GET /api/auth/me` |
| Accounts | `GET`, `POST /api/accounts`; `PATCH`, `DELETE /api/accounts/:id` |
| Categories | `GET`, `POST /api/categories`; `PATCH`, `DELETE /api/categories/:id` |
| Transactions | `GET`, `POST /api/transactions`; `PATCH`, `DELETE /api/transactions/:id` |
| Dashboard | `GET /api/dashboard` |

All endpoints except health, register, and login require an `Authorization: Bearer <token>` header. The React app adds it after sign-in.

## Verification completed

- Prisma client generated successfully.
- Prisma schema validated successfully.
- Backend JavaScript syntax checked successfully.
- API health endpoint tested successfully.
- React production build completed successfully.

This is a complete learning project, not a deployment-ready banking system. Before public deployment, add HTTPS, rate limiting, password-reset flows, stronger validation, automated tests, secure cookie-based sessions, and monitoring.
