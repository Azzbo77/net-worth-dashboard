# Net Worth Dashboard

A single-file, self-hosted net worth tracker with live crypto and stock prices. No backend, no database, no build step — just one HTML file.

## What it does

- Tracks **banking/cash**, **crypto**, **stocks**, and **other investments** (pensions, platform totals, etc.) in one place
- Crypto and stock prices refresh automatically every 60 seconds via the [Finnhub](https://finnhub.io) API
- USD prices are converted to GBP live using [Frankfurter](https://frankfurter.dev) (free, no key required)
- If a ticker isn't supported by Finnhub's free tier (e.g. non-US exchanges like `.TO`, `.L`), the price field falls back to manual entry automatically
- All your data — balances, holdings, API key — is stored in your browser's `localStorage`. Nothing is sent anywhere except live price lookups. Nothing is written back into this file.

## Setup

1. Open `index.html` in a browser (or host it — see below)
2. Get a free API key from [finnhub.io](https://finnhub.io/register)
3. Paste the key into the box at the top of the page — it's remembered from then on
4. Add your accounts, crypto holdings (any ticker, e.g. `BTC`, `ETH`), and US-listed stock tickers (e.g. `AAPL`)

## Hosting it properly

Opening the file directly (`file://`) works, but for reliability across browsers/devices, serve it behind a real web server:

```bash
# nginx / Caddy / your reverse proxy of choice
# just point a location block at this file, e.g.:
caddy file-server --root /path/to/this/folder
```

Or drop it in any static site host — GitHub Pages, Cloudflare Pages, Netlify all work since it's a single static file with no build step.

## Limitations

- **Stocks**: Finnhub's free tier only covers US-listed equities. UK/European/Canadian tickers will show a manual-entry prompt instead of a live price.
- **FX rate**: uses a live USD→GBP rate each refresh cycle; if the FX API is ever unreachable, it falls back to a rough hardcoded rate (0.79) rather than breaking the totals.
- **Rate limits**: Finnhub's free tier allows 60 API calls/minute. Fine for a personal portfolio; if you add a large number of holdings, you may hit this.
- **No sync across devices**: since data lives in browser localStorage, it won't follow you between browsers/devices. If you need that, you'd need to add a small backend — not included here by design (keeps this a zero-dependency single file).

## Editing

It's one HTML file with inline CSS and vanilla JS — no framework, no build tooling. Open it in any text editor to tweak styling, add more crypto/stock rows, or change the refresh interval (`setInterval(fetchAllPrices, 60000)` near the bottom).
