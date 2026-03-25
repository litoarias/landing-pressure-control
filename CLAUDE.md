## Multi-Language Structure — 7 Languages
`index.html` (EN root), `es/`, `fr/`, `de/`, `it/`, `ja/`, `zh/` — each `index.html` is self-contained (no templates/partials). Structural changes must go in all 7 files.

## Non-Obvious Constraints
- `hreflang` alternate links in every page — update all 7 if URL structure changes
- Language auto-detect via `localStorage` (`pc_lang` key) + `navigator.languages`

## Deploy
GitHub Pages at `litoarias.github.io/landing-pressure-control/`
