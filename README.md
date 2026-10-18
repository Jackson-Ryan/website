# Ryan Jackson Website

Personal portfolio website deployed on Cloudflare Workers/Pages using static assets.

## Overview

This repository contains a fully static, single-page portfolio (`index.html`) plus a custom interactive `404.html` page.

The site emphasizes:
- Multi-theme visual design (`paper`, `carbon`, `blueprint`)
- Interactive canvas experiences (physics simulation and generative visuals)
- Lightweight, dependency-free frontend implementation (plain HTML/CSS/JS)
- Cloudflare-native deployment via `wrangler.json`

## Tech Stack

- **Frontend:** HTML5, CSS3, vanilla JavaScript
- **Graphics/Interaction:** HTML Canvas 2D APIs, Web Audio API
- **Hosting/Runtime:** Cloudflare Workers static assets routing (configured via Wrangler)

## Repository Structure

```text
/home/runner/work/website/website
├── index.html       # Main portfolio page with all UI + interaction logic
├── 404.html         # Custom not-found experience with interactive canvas
├── wrangler.json    # Cloudflare deployment/runtime configuration
└── README.md
```

## Core Features

### Main page (`index.html`)
- Sticky nav and command palette (Cmd/Ctrl + K)
- Theme persistence through `localStorage` (`ryan_theme`)
- Optional tactile UI sound effects
- Live UK clock
- Email copy-to-clipboard actions with toast feedback
- Interactive “lab” modes in hero canvas:
  - Lattice spring mesh
  - Dipole field visualization
  - Orbit/gravity particle simulation
- Additional interactive previews for project cards and oscillator controls

### 404 page (`404.html`)
- Shares the same theme system and persisted preference key (`ryan_theme`)
- Displays missing route path dynamically
- Includes an interactive gravitational slingshot canvas

## Development

This is a static site with no build pipeline.

### Quick local preview (any static server)

From `/home/runner/work/website/website`:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

### Cloudflare local dev

From `/home/runner/work/website/website`:

```bash
npx wrangler dev
```

## Deployment

Wrangler configuration is in `wrangler.json`:
- `assets.directory` is set to `./` (repository root)
- `assets.not_found_handling` is set to `404-page`

Deploy with:

```bash
npx wrangler deploy
```

You must be authenticated with Cloudflare (`npx wrangler login`) and have the target account/project configured.

## Customization Notes

- **Theme system:** update CSS variables and the `THEMES`/`THEME_COLORS` constants in `index.html` (and corresponding theme values in `404.html`).
- **Interactive modules:** physics and preview logic are implemented inline in `index.html` script sections.
- **Contact links:** email and social URLs are hardcoded in `index.html` and should be updated together.

## Accessibility and UX

- Semantic landmark elements (`header`, `main`, `section`, `footer`)
- Keyboard shortcut support for command palette
- ARIA roles/labels for dialog and interactive controls
- Responsive layout adaptations for smaller viewports

## Maintenance Checklist

When updating the site:
1. Keep theme tokens synchronized between `index.html` and `404.html`.
2. Verify that interactive canvases still resize correctly after layout changes.
3. Test key interactions:
   - Theme toggle
   - Command palette open/filter/actions
   - Copy-to-clipboard actions
   - Canvas interactivity on desktop and touch devices
4. Validate 404 behavior by requesting a non-existent route in local/preview deployment.