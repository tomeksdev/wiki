---
title: Styling (colors, logo, typography)
parent_shelf: content-authoring
nav_id: content-authoring
category: Authoring
summary: Change colors, logos, and typography through SCSS and assets.
author: Vujca
date: 2025-12-04
---
### Where to edit
- `_scss/_variables.scss`: color tokens (dark and light theme via CSS variables).
- `_scss/_layout.scss`: sidebar, layout spacing.
- `_scss/_components.scss`: cards, hero, buttons, breadcrumbs, theme toggle.
- `_scss/_prose.scss`: typography for article content.
- `assets/vendor/` for third-party CSS/JS (Bootstrap, Font Awesome).

### Rebuilding CSS
Jekyll recompiles SCSS automatically when you run `bundle exec jekyll serve`. For production, run `JEKYLL_ENV=production bundle exec jekyll build`.

### Logos and favicons
- Replace `favicon.ico` and `favicon.png` at the repo root.
- Adjust `.logo-section` styles in `_layout.scss` if you change logo sizing.

### Theme toggle
- The toggle uses `data-theme="dark|light"` on `<html>`. Update color tokens in `_variables.scss` to change palettes.
