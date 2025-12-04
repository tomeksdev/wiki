---
title: Introduction
shelf_id: introduction
nav_id: introduction
nav_title: Introduction
nav_icon: fa-solid fa-book-open
category: Overview
summary: What this wiki template is, how it is organized, and how to use it.
author: TomeksDEV
order: 1
date: 2024-12-04
---
Welcome to the TomeksDEV Wiki template. It is a small Jekyll-powered wiki you can run locally, host on any web server, or publish with GitHub Pages.

## What’s inside
- **Shelves and docs**: Shelves are landing pages, and docs sit underneath each shelf. Add or remove shelves to change the left menu (only Home stays fixed).
- **SCSS-based styling**: Colors, typography, and layout live in `_scss/` and compile to `assets/css/style.css`.
- **Offline-friendly**: Everything is static HTML/CSS/JS; no database is required.

## How to navigate
- The sidebar shows Home plus every shelf in `_shelves/`, ordered with the `order` front matter key.
- Each shelf lists its docs automatically using `parent_shelf` on docs in `_docs/`.
- Contact remains a static page at `/contact/`.
