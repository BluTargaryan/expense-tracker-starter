# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install       # install dependencies (required before first run)
npm run dev       # start dev server at http://localhost:5173
npm run build     # production build to dist/
npm run preview   # preview production build locally
npm run lint      # run ESLint
```

No test runner is configured.

## Architecture

This is a single-page React 19 app built with Vite. There are no routes, no external state management library, and no backend — all data is held in component state and resets on page refresh.

**Data model** — each transaction has: `{ id, description, amount, type, category, date }`. `amount` is always a number. `type` is `"income"` or `"expense"`; `category` is one of `["food", "housing", "utilities", "transport", "entertainment", "salary", "other"]`.

**Component tree:**

```
App                        — owns transactions state; defines categories constant
├── Summary                — receives transactions, computes totalIncome/totalExpenses/balance internally
├── TransactionForm        — owns form field state; calls onAdd(transaction) prop on submit
└── TransactionList        — receives transactions; owns filterType/filterCategory state and filter logic
```

`categories` is defined as a module-level constant in `App.jsx` and passed as a prop to both `TransactionForm` and `TransactionList`.

**Known intentional issue** (this is a course starter meant to be fixed):
- Transaction #4 ("Freelance Work") is marked `type: "expense"` but `category: "salary"` — a data inconsistency.
- The UI has minimal styling and no delete/edit functionality.

## Styling

Global styles are in `src/index.css`; component-scoped styles are in `src/App.css`. CSS class names like `.income-amount` and `.expense-amount` are reused for both the summary cards and the transaction table rows.
