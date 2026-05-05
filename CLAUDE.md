# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a single-page static website for **The Place**, an Italian restaurant in Roseville, CA. The entire site lives in one file: `index.html`.

## Development & Deployment

There is no build step, package manager, or local dev server. To preview:

```bash
open index.html        # macOS — opens directly in browser
python3 -m http.server # optional: serve locally at http://localhost:8000
```

Deployment is automatic: pushing to `main` triggers the GitHub Actions workflow (`.github/workflows/static.yml`) which deploys to GitHub Pages.

## Architecture

**Everything is in `index.html`** — CSS in a `<style>` block in `<head>`, JavaScript inline at the bottom of `<body>`, and all markup in between. There are no external `.css` or `.js` files.

### CSS structure

Design tokens are defined as CSS custom properties at the top of the `<style>` block under `/* CUSTOM PROPERTIES */`. Modify colors, the nav height (`--nav-h`), etc. there first. Sections follow in order: nav → hero → menu → order CTA → about → contact → dahlia strip → footer → responsive breakpoints.

### Page sections (HTML `id`s)

| `id` | Description |
|------|-------------|
| `nav` | Fixed navbar; adds `.scrolled` class via scroll listener |
| `hero` | Full-viewport hero with zoom animation |
| `menu` | Tabbed menu — tabs use `data-tab` attribute, panels use `id="tab-{name}"` |
| `order` | Order CTA with parallax background |
| `reservations` | Reservations strip linking to Tock |
| `about` | Two-column story section |
| `contact` | Three-column grid: hours / location / order |
| `dahlia-flowers` | Partner section for Totally Tubers |
| `footer` | Address, social, copyright |

### JavaScript (inline, bottom of `<body>`)

Three behaviours only:
1. Nav scroll state — toggles `.scrolled` on `#nav`
2. Hamburger / mobile menu toggle — `.open` class on `#mobile-menu` and `#hamburger`
3. Menu tabs — activates matching `.menu-panel` by `data-tab` → `id="tab-{name}"`
4. Hours highlight — adds `.today` class to the current day's `.hours-row`

### Images (`images/`)

| File | Used for |
|------|----------|
| `logo.webp` | Nav, hero, footer |
| `hero.jpg` | Hero background |
| `dahlia-totally-tubers-bg.png` | Dahlia section background |
| `totally-tubers-logo.png` | Partner logo in dahlia section |

The order CTA background and the about section image are loaded from Unsplash URLs directly in the HTML.

## External services

- **Ordering**: Square — `https://theplaceroseville.square.site`
- **Reservations**: Tock — `https://www.exploretock.com/the-place-roseville`
- **Full menu PDF**: hosted at `thatlittleitalianplace.com`
- **Google Maps**: directions link in contact section
- **Fonts**: Google Fonts (Playfair Display, Crimson Pro)
