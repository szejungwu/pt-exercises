# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-page PWA (Progressive Web App) that displays physical therapy exercises prescribed across two PT sessions. The site is hosted on GitHub Pages at `https://szejungwu.github.io/pt-exercises/` and works offline on mobile devices.

## Architecture

- **`index.html`** — The entire app: data, UI, styles, and logic in one self-contained file. Exercise data is stored as a JavaScript array. Filtering logic (by session and category) is vanilla JS with no dependencies.
- **`sw.js`** — Service worker for offline caching (network-first, fallback to cache).
- **`manifest.json`** — PWA manifest for home screen installation.
- **`icon-192.png` / `icon-512.png`** — PWA icons.

## Data Source

Exercise data originates from two Word documents in `~/AI Projects/`:
- `PT Session 1.docx` — 6 categories, ~30 exercises
- `PT Session 2.docx` — 4 categories, ~25 exercises

Each exercise has: name, session number, category, target/goal, parameters & cues, frequency/reps, and resource links (YouTube videos, PDFs, tools).

## Development

No build step. To preview locally:

```bash
cd pt-exercises && python3 -m http.server 8080
```

Then open `http://localhost:8080`.

## Deployment

Hosted via GitHub Pages (legacy mode, `main` branch, root `/`). Push to `main` to deploy:

```bash
git push origin main
```

GitHub repo: `szejungwu/pt-exercises`

## Key Design Decisions

- **Category-level tags** (not individual exercise names) are used as the second filter row. Categories match the section headers from the original Word documents (e.g., "Vestibular & Face", "Neck & Upper Body Mobility").
- **Session + Category filtering** are independent and combinable. Selecting a session narrows the visible category tags.
- When updating the service worker cache, bump `CACHE_NAME` version in `sw.js`.
