# Portfolio Tracker — Requirements

## Overview

A private, mobile-first web app for tracking a personal stock & ETF portfolio. Fully client-side — no backend, no server, no accounts. Your data stays on your device. Ships as a single HTML file with embedded CSS and JS.

## Core Principles

- **Private & secure** — no server, no backend, no tracking. Your portfolio data never leaves your device.
- **localStorage only** — all data stored locally in the browser. Nothing is sent or synced anywhere.
- **Single file** — ship as one `index.html` (CSS & JS embedded). No build step, no dependencies.
- **Mobile-first** — designed for phone screens; usable on desktop too
- **Start simple** — MVP first, iterate from there

## Data Model

Three collections stored in `localStorage`:

### Items (`portfolio_items`)
Each item is a specific holding in a specific account:
```json
{
  "id": 1234567890,
  "symbol": "AAPL",
  "shares": 10,
  "accountId": 9876543210
}
```
The same symbol can appear in multiple accounts.

### Accounts (`portfolio_accounts`)
```json
{
  "id": 9876543210,
  "name": "Roth IRA"
}
```

### Prices (`portfolio_prices`)
Cached prices keyed by symbol:
```json
{
  "AAPL": { "price": 185.50, "lastUpdated": 1707600000000 }
}
```

## Features (v0.2)

### Tabbed Interface
Three tabs: **Holdings**, **Items**, **Accounts**

### 1. Holdings Tab (aggregated view)
- Groups items by **symbol** across all accounts
- Shows per-symbol: total shares, price, market value, account badges
- **Tap symbol** to open its Yahoo Finance page for detailed quotes & news
- Read-only summary — editing happens in the Items tab

### 2. Items Tab (detailed view)
- Lists every individual item: symbol + account + shares
- **Add item**: symbol, shares, account (dropdown from accounts list)
- **Edit item**: change symbol, shares, or account
- **Edit shares**: tap shares to quick-edit via prompt
- **Delete item**: remove with confirmation

### 3. Accounts Tab
- Lists all accounts with total value and item count
- Shows "Unassigned" group for items with no account
- **Add account**: name input
- **Edit account**: rename via prompt
- **Delete account**: removes account, items become unassigned

### 4. Refresh Prices
- A single **"Refresh Prices"** button (always visible above tabs)
- Fetches current prices for all unique symbols via CORS-proxied Yahoo Finance v8
- Updates cached prices in `portfolio_prices`
- Shows spinner during fetch, toast with result count

### 5. Summary Card
- Always visible at top: **total portfolio value**
- Shows count of symbols, items, and accounts

### 6. Persistence
- All changes immediately saved to `localStorage`
- On load, data restored from `localStorage`
- Automatic migration from v0.1 data format

## UI / UX

- Clean, minimal card-based layout
- Three-tab navigation with pill-style active indicator
- Large tap targets for mobile
- System font stack for fast rendering
- Account names shown as small badges on cards
- Responsive: works on 320px–768px widths
- Apple touch icon + web app meta tags for iOS home screen

## Price Data Source

- Primary: Yahoo Finance v8 endpoint via `corsproxy.io`
- Fallback: `allorigins.win` CORS proxy
- Prices fetched on demand only (no polling)
- Prices stored separately from items (shared across accounts)

## Non-Goals (for now)

- No authentication / user accounts
- No purchase price / cost basis tracking (future)
- No charts or historical data (future)
- No notifications or alerts
- No PWA / offline mode (future)
- No build tools, bundlers, or frameworks

## Future Iterations (ideas)

- Cost basis & gain/loss per holding
- Sorting / filtering holdings
- Currency formatting options
- Multiple portfolios
- Import / export (JSON or CSV)
- Dark mode
- PWA with offline support
