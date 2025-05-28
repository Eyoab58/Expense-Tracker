# Vue Expense Tracker

A simple expense tracker web application built with Vue 3 and Vite. This app allows users to add, view, and delete transactions, and keeps a running balance of income and expenses. Data is persisted in the browser using localStorage.

## Technologies Used

- **Vue 3**: The progressive JavaScript framework for building user interfaces.
- **Vite**: Next Generation Frontend Tooling for fast development and hot module replacement.
- **JavaScript (ES6+)**: Core language for logic and interactivity.
- **vue-toastification**: For beautiful toast notifications.
- **localStorage**: For client-side data persistence.
- **CSS**: For basic styling.

## Features

- Add new transactions (income or expense)
- View a running balance, total income, and total expenses
- Delete transactions
- Data persists across browser reloads
- Toast notifications for user feedback

## Demo

<!-- Place your screen recording or demo link here -->

## Getting Started

1. **Install dependencies:**
   ```sh
   npm install
   ```
2. **Run the development server:**
   ```sh
   npm run dev
   ```
3. **Open your browser:**
   Visit [http://localhost:5173](http://localhost:5173) (or the port shown in your terminal)

## Project Structure

- `src/` - Main source code
  - `components/` - Vue components (Header, Balance, IncomeExpenses, TransactionList, AddTransaction)
  - `App.vue` - Main app component
  - `main.js` - App entry point
- `public/` - Static assets
- `package.json` - Project metadata and scripts