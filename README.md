# 📊 Client Payment Tracker — 2026–2031

A live insurance premium payment monitoring dashboard, hosted on GitHub Pages.

## Features

- **Live data** — reads directly from your Google Sheet via the GViz API (no backend needed)
- **Year tabs** — switch between 2026–2031 payment sheets
- **Quick stats** — counts of Paid / Pending / Past Due / Lapsed across the active year
- **Search & filter** — find clients by name or filter by payment status
- **Summary row** — per-month status counts at the bottom of the table
- **Auto-refresh** — data reloads every 5 minutes

## Setup

### 1. Make your Google Sheet public

In Google Sheets → Share → Change to **"Anyone with the link"** → **Viewer**.

### 2. Verify the Sheet ID

The Sheet ID in `index.html` is:
```
15mhNWjxg07pEgvwoGkWOnNFt5UEpDhAerV4Q1PUnmQM
```

This matches your existing spreadsheet. If you move the data, update `SHEET_ID` in the `<script>` section.

### 3. Deploy to GitHub Pages

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/client-payment-tracker.git
git push -u origin main
```

Then go to your repo → **Settings → Pages → Source → Deploy from branch → main → / (root)** → Save.

Your site will be live at:
```
https://YOUR_USERNAME.github.io/client-payment-tracker/
```

## Sheet Structure Expected

| Column | Content |
|--------|---------|
| A | Row # / Client ID |
| B | Client Name |
| C–N | Jan–Dec payment status |

Status values: `Paid`, `Pending`, `Past Due`, `Lapsed`

## Local Development

Just open `index.html` in a browser. No build step required.
