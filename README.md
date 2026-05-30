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
- Profit margin slider (0–200%).
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
- **EN / ID language switch** (English default).
- **Product templates** — save the current setup and reload it later.
- Indonesian Rupiah formatting throughout.

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

## Known limitation: templates do not persist yet

Saved templates are kept **in memory only**, so they reset when the page is
reloaded. This is intentional for the current sandboxed build.

To make them persistent once deployed, store them in the browser with
`localStorage` (or a backend). The save/load logic lives in
`renderTemplates()` / `loadTemplate()` in the `<script>` block — persisting the
`state.templates` array there is a small change.

---

## Notes
- The **Tax / PPN** field has no default rate. Set the current Indonesian PPN
  rate yourself before relying on it for anything official.
- Tech: plain HTML + CSS + vanilla JavaScript. Font: Inter (Google Fonts).
