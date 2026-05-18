# Crypto Regulatory Atlas

Interactive single-page visualization of the global crypto regulatory landscape. 27 jurisdictions across 5 regions, each with a click-through dossier.

![Status: static-site](https://img.shields.io/badge/site-static-blue) ![Build: none](https://img.shields.io/badge/build-none-green)

## What's in it

- **Interactive world map** with status-colored country pins (licensed / restricted / banned)
- **Per-country dossier panel** covering regulators, framework, license types, key requirements, and an operator-level practical note
- **Regional card grid** (Americas, Europe, MENA, APAC, Africa) for fast browsing
- **Filter chips + search** across country names and regulators
- **Live stat counters** for licensed / restricted / banned jurisdictions

## Stack

Zero dependencies. One file. Just open `index.html` in a browser.

- Pure HTML / CSS / vanilla JS
- SVG world map generated client-side from lat/lng data
- Google Fonts: Instrument Serif, IBM Plex Mono, IBM Plex Sans

## Local preview

```bash
# Simplest — just open the file
open index.html

# Or serve with any static server
python3 -m http.server 8000
# → http://localhost:8000
```

## Deploy

### Vercel (recommended)

```bash
npm i -g vercel
vercel login
vercel --prod
```

Or push to GitHub and connect the repo via the Vercel dashboard. `vercel.json` is already configured. No build step, no environment variables.

### Other platforms

Works as-is on Netlify, Cloudflare Pages, GitHub Pages, or any static host. Point at the repo root.

## Editing the data

All regulatory data is in the `countries` array inside `index.html`. See `AGENTS.md` for the schema and conventions.

## Disclaimer

Data reviewed May 2026. Regulatory landscapes shift fast — verify with counsel before acting on anything you read here.
