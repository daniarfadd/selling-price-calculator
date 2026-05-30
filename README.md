# Sales Price Calculator

A minimalist, mobile-first web app that helps small business owners and makers
(tailors, craftspeople, UMKM sellers) work out a fair selling price from their
production cost and desired profit. Built as a single, dependency-free HTML file.

---

## Features

### Simple mode
- Add cost items (name + amount), edit or delete any of them inline.
- Automatic **Total Production Cost**.
- **Pieces produced** stepper — split a batch cost across N units to get the
  per-piece selling price (e.g. Rp 5.000.000 ÷ 12 pieces, +50% margin →
  **Rp 625.000 / piece**, Rp 7.500.000 batch total).
- **Forward / Reverse** switch:
  - *Forward* — set a margin with the slider, get the selling price.
  - *Reverse* — type a target or competitor selling price and instantly see the
    margin it implies and your profit (per piece and for the batch). Selling
    below cost shows a negative margin in red.
- Real-time selling price.

### Advanced mode
- **Materials** with quantity × unit cost per product.
- **Labor** (hours × rate) and **overhead** (total ÷ batch size, per unit).
- **Markup vs Margin** toggle — markup adds on top of cost; margin is true
  profit ÷ selling price (capped below 100%).
- **Marketplace + payment fees** — listing price is grossed up so your target
  profit survives platform cuts.
- **Tax / PPN** added on top for the customer.
- Full per-unit breakdown: base cost, profit, fees, tax, what you receive,
  and real margin %.

### Everywhere
- **Discount simulator** — see what a flash-sale discount does to your profit
  and margin, plus the **break-even discount** (the point where profit hits
  zero). Works in both modes and accounts for marketplace fees and tax in
  Advanced. Selling below cost is flagged in red.
- **Export as PDF** — generates a clean, itemized quote / costing sheet in the
  active language and mode, with an optional business name. Uses the browser's
  built-in *Save as PDF*, so no libraries and it works offline.
- **Dark / light mode toggle** — remembers your choice and follows your
  system preference on first visit.
- **EN / ID language switch** (English default).
- **Product templates** — save the current setup and reload it later.
- Indonesian Rupiah formatting throughout.

---

## Exporting a PDF quote

Tap **Export as PDF** at the bottom. The app builds a clean, itemized document
from your current calculation — respecting the active mode (Simple = price
quote, Advanced = costing sheet) and language — then opens the browser's print
dialog. Choose **Save as PDF** (or print directly). Add a business/shop name in
the field above the button to brand the header; it's remembered for next time.

This relies on the browser's native print-to-PDF, so there's no extra library
to load and it works offline.

---

## Install as an app & offline use (PWA)

The app is a Progressive Web App, so it can be installed to a phone or desktop
and used **without an internet connection** after the first load.

- **Desktop (Chrome/Edge):** open the served URL, then click the install icon in
  the address bar.
- **Android (Chrome):** menu → *Add to Home screen* / *Install app*.
- **iOS (Safari):** Share → *Add to Home Screen*.

Once installed it launches full-screen with its own icon. A service worker
(`sw.js`) caches the app shell, and the Inter font is cached after the first
online visit, so everything keeps working offline (it falls back to the system
font if the font was never cached).

**Important:** the service worker only activates when the app is served over
`http://` or `https://` (a local server or a real host) — not when opening the
file directly with `file://`. Use the local-server option below, or deploy it,
to get install + offline behavior. To ship an update, bump the `CACHE` version
string at the top of `sw.js`.

---

## How to run it locally

The app is a single static file with no build step and no dependencies.

### Option 1 — just open it
Unzip the archive and double-click **`index.html`**. It opens in any modern
browser. An internet connection is only needed to load the Inter font from
Google Fonts; all calculations run locally.

### Option 2 — run a local web server (recommended)
Serving over `http://` behaves more like a real deployment. From the unzipped
folder:

**Python 3** (already installed on most machines):
```bash
python3 -m http.server 8000
```
Then open <http://localhost:8000> in your browser.

**Node.js** (if you have it):
```bash
npx serve .
```
Then open the URL it prints (usually <http://localhost:3000>).

---

## Deploying online

Because it is a single static file, you can host it for free on:
- **Netlify** or **Vercel** — drag the folder onto their dashboard.
- **GitHub Pages** — push the file to a repo and enable Pages.

No server-side code is required.

---

## Templates & saved data

Saved templates and your theme choice are stored in the browser with
`localStorage`, so they persist across reloads and visits on the same device.

Storage access is wrapped in a safe fallback: if a browser (or a sandboxed
preview) blocks `localStorage`, the app keeps everything in memory for the
session instead of throwing an error — it just won't persist after a reload in
that environment.

Stored keys: `spc-templates` (saved templates) and `spc-theme` (light/dark).
The logic lives in `persistTemplates()` / `loadTemplatesFromStorage()` and the
`safeGet` / `safeSet` helpers in the `<script>` block. To move to multi-device
sync later, swap those helpers for backend calls.

---

## Notes
- The **Tax / PPN** field has no default rate. Set the current Indonesian PPN
  rate yourself before relying on it for anything official.
- Tech: plain HTML + CSS + vanilla JavaScript. Font: Inter (Google Fonts).
