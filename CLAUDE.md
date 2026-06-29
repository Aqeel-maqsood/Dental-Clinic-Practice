# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file static dental clinic landing page (`index.html`). No build tools, no dependencies, no package manager — everything lives in one self-contained HTML file with embedded CSS and JavaScript.

## Running the Site

Open `index.html` directly in a browser. No server required. For live-reload during development, use any static server:

```bash
# Python (built-in)
python -m http.server 8080

# Node (if npx available)
npx serve .
```

## Architecture

Everything is in `index.html` in this order:

1. **`<style>` block** — all CSS using custom properties defined in `:root`. Layout uses CSS Grid and `clamp()` for fluid responsiveness. No media query spaghetti — breakpoints only at 900px and 640px.
2. **HTML body** — sections flow top to bottom: floating call button → toast → navbar → hero → trust bar → services → why-us → testimonials → team → offer banner → FAQ → contact → map → footer.
3. **`<script>` block** — vanilla JS at the bottom. Three behaviors: mobile nav toggle, FAQ accordion, form submit toast.

## Design Tokens (CSS Variables)

All colors and spacing are in `:root`. Change here to restyle the whole page:

| Variable | Value | Used for |
|---|---|---|
| `--blue` | `#1a6fdb` | Primary brand, CTAs, links |
| `--teal` | `#0cb8b6` | Floating call button, accents |
| `--gold` | `#f59e0b` | Star ratings |
| `--radius` | `12px` | Card border radius |

## Key Customizations

When adapting for a real clinic, replace:

- **Clinic name**: `BrightSmile Dental` (appears in `<title>`, navbar, hero, footer)
- **Phone**: `(555) 123-4567` / `tel:+15551234567` (navbar, floating button, contact section)
- **Address**: `123 Smile Avenue, Suite 200, New York, NY 10001`
- **Email**: `hello@brightsmile.com`
- **Doctor names/bios**: in the `#team` section
- **Map placeholder**: replace `.map-placeholder` div with a Google Maps `<iframe>` embed
- **Form action**: both `#heroForm` and `#contactForm` currently only show a toast — wire to a backend or service like Formspree

## Forms

Both forms (`#heroForm` in the hero card, `#contactForm` in the contact section) are purely frontend. On submit they call `showToast()` and reset. To make them functional, add a `fetch()` POST inside the submit handler or replace with a form service embed.

## GitHub Pages Hosting

This repo can be served for free via GitHub Pages:
Settings → Pages → Source: `main` branch → root folder → Save.
URL: `https://aqeel-maqsood.github.io/Dental-Clinic-Practice/`
