# Portfolio Tracker — Requirements

## Overview

A mobile-first, client-side-only web app for tracking a personal stock & ETF portfolio. No backend, no build step — just a single HTML file with embedded CSS and JS that runs in a mobile browser.

## Core Principles

- **Zero backend** — everything runs in the browser
- **localStorage only** — all portfolio data persists in `localStorage`
- **Mobile-first** — designed for phone screens; usable on desktop too
- **Single file** — ship as one `index.html` (CSS & JS embedded)
- **Start simple** — MVP first, iterate from there

## Data Model

Each holding is stored as an object:

```json
{
  "symbol": "AAPL",
  "shares": 10,
  "price": null,
  "lastUpdated": null
}
```

The full portfolio is an array of holdings, stored in `localStorage` under the key `portfolio`.

## MVP Features (v0.1)

### 1. View Portfolio
- Display a list/table of all holdings: **symbol**, **shares**, **price**, **market value** (shares × price), **last updated**
- Show a **total portfolio value** at the top

### 2. Add Holding
- Simple form: symbol (text input) + shares (number input)
- Adds to the portfolio list and saves to localStorage
- Duplicate symbols should update the existing entry's share count

### 3. Remove Holding
- Each row has a delete button to remove the holding

### 4. Edit Shares
- Tap on shares to edit the quantity inline or via a prompt

### 5. Refresh Prices
- A single **"Refresh Prices"** button fetches current prices for all holdings
- Uses a free, no-auth API (Yahoo Finance v8 quote endpoint via a CORS proxy, or similar)
- Updates price and lastUpdated for each holding
- Shows a loading indicator during fetch

### 6. Persistence
- All changes are immediately saved to `localStorage`
- On page load, portfolio is restored from `localStorage`

## UI / UX

- Clean, minimal card-based or list-based layout
- Large tap targets for mobile
- System font stack for fast rendering
- Color-coded gain/loss indicators (future iteration)
- Responsive: works on 320px–768px widths

## Price Data Source

- Primary: Yahoo Finance v8 endpoint via `query1.finance.yahoo.com`
- Fallback plan: swap to another free API if Yahoo blocks requests
- Prices fetched on demand only (no polling)

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
