# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML/CSS/JS landing page for **Pressure Control**, an iOS blood pressure monitoring app. No build system or package manager — files are served directly.

Deployed via GitHub Pages at: `https://litoarias.github.io/landing-pressure-control/`

## Architecture

### Multi-language Structure

The site supports 7 languages. English is the root, and each other language lives in its own subdirectory:

```
index.html          ← English (root/default)
es/index.html       ← Spanish
fr/index.html       ← French
de/index.html       ← German
it/index.html       ← Italian
ja/index.html       ← Japanese
zh/index.html       ← Chinese
```

Each `index.html` is a **complete, self-contained page** — there is no templating or shared HTML partials. When making content or structural changes, you must apply them to all 7 files.

### Language Auto-Detection

Each `index.html` includes an inline `<script>` at the top that reads `localStorage` (`pc_lang` key) and browser `navigator.languages` to auto-redirect non-English users to the appropriate subdirectory.

### Asset Paths

- Root-level `index.html` references assets as `assets/...` and content as `content/...`
- Subdirectory pages (e.g. `es/index.html`) reference assets as `../assets/...` and content as `../content/...`

### CSS

Single stylesheet at `assets/style.css`. Uses:
- **BEM methodology** for class naming (`.nav__link`, `.hero__title`, etc.)
- **CSS custom properties** for theming — light/dark mode via `prefers-color-scheme` media query and a `.dark-mode` class on `<body>`
- Inter font from Google Fonts

### JS Libraries

- `assets/tobi.min.js` + `assets/tobi.css` — Tobi lightbox for screenshot gallery (no other JS dependencies)

## Development

No build step required. Open any `index.html` directly in a browser, or serve the root with any static server:

```bash
python3 -m http.server 8080
# or
npx serve .
```

## Key Constraints

- **All 7 language files must stay in sync** for structural/layout changes.
- The CSS stylesheet is loaded from an absolute URL in root `index.html` (`https://litoarias.github.io/landing-pressure-control/assets/style.css`) — subdirectory pages use relative paths (`../assets/style.css`). Keep this distinction when editing `<head>`.
- `hreflang` alternate links are present in every page for SEO — update all pages if the URL structure changes.
