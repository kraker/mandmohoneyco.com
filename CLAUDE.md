# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static website for M. & Mo. Honey Co. LLC (mandmohoneyco.com) — a honey and beeswax products business in Tulsa, OK. Built with Hugo, deployed to GitHub Pages.

Owners: Paul Kirby (beekeeper, majority owner) and Alex Kraker (business partner).

## Build & Development

```bash
hugo server -D          # Local dev server with drafts at localhost:1313
hugo                    # Build to public/
hugo --gc --minify      # Production build (what CI runs)
```

Deployment is automated via GitHub Actions on push to `main`. No manual deploy needed.

## Architecture

**Custom theme** (no external theme dependency) — all layouts and styles live in the project root, not under `themes/`.

- `hugo.yaml` — Site config: baseURL, nav menu, site params (tagline, phone, address)
- `data/products.yaml` — Product catalog. This is the single file to edit for product/price changes. Categories, items, sizes, prices, scent/flavor variants.
- `assets/css/main.css` — All styles in one file using CSS custom properties for brand tokens (colors, fonts, spacing)
- `layouts/` — Custom templates. Key files:
  - `index.html` — Home page (hero with beehive illustration, category overview)
  - `_default/products.html` — Products page, iterates `data/products.yaml`
  - `_default/single.html` — Generic page (About, Contact)
  - `partials/product-card.html` — Renders a single product with conditional scents/flavors
- `content/` — Four pages: `_index.md` (home), `products.md` (uses `layout: products`), `about.md`, `contact.md`
- `static/images/` — Beehive illustrations extracted from Canva branding PDFs
- `resources/` — Source branding files (pptx, xlsx, zip) — gitignored, local reference only

## Brand Design

Colors extracted from Canva product labels:
- Cream background (`#ECE6DB`), charcoal text (`#282828`), gold accent (`#946B09`), tan borders (`#D4C5AF`)

Fonts (Google Fonts, chosen to approximate Canva brand fonts Roxborough CF / Dream Avenue / Glacial Indifference):
- Headings: Playfair Display
- Tagline/script: Dancing Script
- Body: Raleway

## Key Conventions

- Image paths in templates must use `{{ "images/file.png" | relURL }}` — not hardcoded `/images/...` — for GitHub Pages compatibility
- Product data lives in `data/products.yaml`, not in content files
- The `products.md` content file uses `layout: "products"` in front matter to select the custom layout
- The workflow builds with the `baseURL` from `hugo.yaml` (not the Pages action output) because the site uses a custom domain
- `static/CNAME` must contain `mandmohoneyco.com` for GitHub Pages custom domain
