---
title: Shelves
parent_shelf: content-authoring
nav_id: content-authoring
category: Authoring
summary: Understand shelf fields and how docs attach to them.
author: Vujca
date: 2025-12-04
---
Each shelf is a landing page plus metadata used for the sidebar.

### Required fields
- `shelf_id`: unique handle used by docs.
- `nav_id`: used to highlight the active item in the sidebar (usually the same as `shelf_id`).
- `order`: numeric sort order in the sidebar.
- `title` / `nav_title`: page heading and sidebar label.

### Optional fields
- `nav_icon`: Font Awesome icon (e.g., `fa-solid fa-book-open`).
- `category`, `summary`, `author`, `date`: displayed on cards and shelf pages.

### Attaching docs
- Set `parent_shelf: <shelf_id>` on docs in `_docs/`.
- Shelf pages automatically list all attached docs at the bottom.
