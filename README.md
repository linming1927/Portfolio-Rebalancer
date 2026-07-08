# Portfolio Rebalancer

A browser-based tool for rebalancing an investment portfolio against custom target allocations — no backend, no account, no data ever leaves your browser.

## What it does

- **Import holdings** directly from a Morningstar portfolio export (`.xlsx`) — no reformatting needed
- **Group holdings** into custom categories (e.g. US Index, Ex-US Index, Bonds, Individual Stocks) with your own ticker-to-group rules
- **Two-level rebalancing:**
  1. Set target % at the group level, see how to split new cash (or a full rebalance) across groups
  2. Drill into any group and repeat at the individual holding level
- **Buy-only or full rebalance:** choose between directing new cash toward underweight positions only, or a full rebalance that includes selling overweight positions
- **Persistent targets:** your group definitions and target percentages are saved automatically — only your holdings refresh each time you re-import

## Privacy

Everything runs client-side. Your holdings, values, and targets are stored only in your browser's local storage — nothing is uploaded, logged, or sent to any server. The source code itself contains no personal data.

## Running it

This is a single self-contained HTML file — no build step, no dependencies to install.

1. Download `portfolio-rebalancer-standalone.html`
2. Open it in any modern browser (double-click, or serve it locally with `python3 -m http.server`)

Or host it directly from this repo via **GitHub Pages** (Settings → Pages → deploy from main branch) for a stable URL you can bookmark.

A React (`.jsx`) version is also included for anyone who wants to build on it with a standard toolchain (e.g. Vite).

## How the rebalancing math works

Given your current holdings, target percentages, and an amount of cash to deploy (which can be $0 for a pure rebalance):

- **Buy-only mode:** directs cash toward whatever is most underweight first. If your contribution fully closes every gap, the remainder is spread proportionally by target weight so nothing gets overshot.
- **Full rebalance mode:** calculates the exact buy or sell amount for every holding needed to land precisely on target, given the new total (current holdings + cash in).

## Tech

Plain React (loaded via CDN, JSX transpiled in-browser with Babel Standalone) and [SheetJS](https://sheetjs.com/) for reading `.xlsx` files. No build tooling required to run the standalone version.
