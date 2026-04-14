# mandmohoneyco.com

Public facing website for **M. & Mo. Honey Co. LLC** at [mandmohoneyco.com](https://mandmohoneyco.com).

*Created by critters, Crafted by hand.*

## About

M. & Mo. Honey Co. is a locally owned and operated honey and beeswax products company based in Tulsa, Oklahoma. This site serves as our online presence for product information and pricing.

## Tech Stack

- **[Hugo](https://gohugo.io/)** static site generator (v0.152.2 extended)
- Custom theme (no external theme dependency)
- Deployed to **GitHub Pages** via GitHub Actions
- Custom domain via Cloudflare DNS

## Local Development

```bash
# Install Hugo (Fedora)
sudo dnf install hugo

# Run dev server with drafts
hugo server -D

# Production build
hugo --gc --minify
```

The dev server runs at `http://localhost:1313` with live reload.

## Updating Products & Pricing

All products and prices are managed in a single file: [`data/products.yaml`](data/products.yaml). Edit this file to add, remove, or update products. Changes pushed to `main` deploy automatically.

## Deployment

Pushes to `main` trigger the GitHub Actions workflow (`.github/workflows/hugo.yaml`) which builds the site and deploys to GitHub Pages. No manual deployment steps needed.

## Project Structure

```text
content/           Markdown pages (home, products, about, contact)
data/              Product catalog (products.yaml)
layouts/           Hugo templates and partials
assets/css/        Stylesheet (main.css)
static/images/     Beehive illustrations and brand assets
resources/         Source branding files from Canva (not tracked in git)
```
