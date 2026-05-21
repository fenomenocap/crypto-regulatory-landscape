# AGENTS.md

Instructions for Codex (and other coding agents) working on this repository.

## Project

**Crypto Regulatory Atlas** — a single-page interactive visualization of the global crypto regulatory landscape. 30 jurisdictions tracked across 5 regions, each with a clickable dossier covering regulators, frameworks, license types, key requirements, and operator notes.

## Architecture

This is a **zero-dependency static site**. Everything lives in `index.html`:

- All HTML, CSS, and JavaScript inlined in a single file
- No build step
- No external JS libraries
- Only external resource: Google Fonts (Instrument Serif, IBM Plex Mono, IBM Plex Sans)
- Country data is a JavaScript array inside the HTML; SVG world map and country pins are generated client-side

Do **not** add a bundler, framework, or build pipeline unless explicitly asked. The static-file simplicity is intentional.

## Deployment

Target platform: **Vercel** (static hosting). `vercel.json` is already configured.

### Deploy steps

1. Initialize git if not already: `git init && git add . && git commit -m "Initial commit"`
2. Push to a GitHub repository
3. Either:
   - Connect the repo to Vercel via the dashboard and deploy, or
   - Run `vercel --prod` from this directory (requires `npm i -g vercel` and `vercel login` first)

No environment variables required. No build command needed (Vercel will detect the static site automatically).

### Alternative platforms

This will also work as-is on Netlify, Cloudflare Pages, GitHub Pages, or any static host. Just point the host at the repo root.

## Editing the regulatory data

Country data lives in the `countries` array inside `index.html` (search for `const countries = [`). Each entry follows this shape:

```js
{
  id: 'xx',                      // lowercase ISO-style code
  name: 'Country Name',
  flag: '🇽🇽',
  region: 'Americas' | 'Europe' | 'MENA' | 'APAC' | 'Africa',
  lat: 0,                        // for map pin placement
  lng: 0,
  status: 'licensed' | 'payment-restricted' | 'transitional' | 'restricted' | 'banned',
  regulators: 'AAA · BBB · CCC', // ' · ' separated
  tagline: 'One-line summary for the card.',
  summary: 'Italicized blockquote at the top of the dossier panel.',
  framework: 'Paragraph on the regulatory framework.',
  licenseTypes: 'Paragraph listing license categories.',
  requirements: [
    'Numbered requirement 1',
    'Numbered requirement 2',
    // ...
  ],
  practical: 'Operator-note callout. The honest take.',
  lastReviewed: 'May 2026',       // optional; displayed in the dossier
  sources: [                      // optional; displayed as source-review links
    { label: 'Regulator guidance', url: 'https://example.gov/guidance' }
  ]
}
```

Adding a country automatically updates: the world map pin, the stat counters at the top, the regional card grid, and the search/filter logic. Add source-review links either directly on the country entry or in the `sourceRegistry` object keyed by country `id`.

If a country pin overlaps with another or its label clashes, adjust the `labelOffsets` object further down in the same file (`dx`, `dy` from the pin).

## Style/aesthetic conventions

If asked to extend or restyle, preserve:

- **Dark editorial** aesthetic — warm cream text (`--text-primary: #f5f1e8`) on near-black (`--bg: #0c0c0e`), warm amber accent (`--accent: #d4a574`)
- **Typography pairing** — Instrument Serif for display, IBM Plex Mono for labels/metadata, IBM Plex Sans for body
- **Status color system** — green/blue/purple/amber/red for licensed/payment-restricted/transitional/restricted/banned, used consistently across map pins, card border, status pills, and panel header
- **Mono-uppercase labels** with wide letter-spacing for any metadata or eyebrow text

Avoid: generic SaaS gradients, rounded-everything design, sans-only typography, default Tailwind/shadcn aesthetic.

## Things to avoid

- Don't introduce a build tool (Vite, Next.js, etc.) unless explicitly asked
- Don't split into multiple files unless explicitly asked
- Don't replace the inline data with a fetched JSON file unless explicitly asked — keeping it inline means zero-runtime-failure deployment
- Don't add analytics, tracking, or third-party scripts without asking
- Don't change the editorial color palette or typography without asking
