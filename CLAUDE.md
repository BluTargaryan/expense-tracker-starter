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

This is a single-page React 19 app built with Vite. All application logic lives in one file: `src/App.jsx`. There are no routes, no external state management library, and no backend — all data is held in component state and resets on page refresh.

**Data model** — each transaction has: `{ id, description, amount, type, category, date }`. `type` is `"income"` or `"expense"`; `category` is one of `["food", "housing", "utilities", "transport", "entertainment", "salary", "other"]`.

**Known intentional issues** (this is a course starter meant to be fixed):
- `amount` is stored as a string but used directly in `.reduce()` arithmetic, causing string concatenation instead of numeric addition — totals display incorrectly.
- Transaction #4 ("Freelance Work") is marked `type: "expense"` but `category: "salary"` — a data inconsistency.
- The UI has minimal styling and no delete/edit functionality.

## Styling

Global styles are in `src/index.css`; component-scoped styles are in `src/App.css`. CSS class names like `.income-amount` and `.expense-amount` are reused for both the summary cards and the transaction table rows.
