---
title: Adding a detailed doc beneath a shelf
parent_shelf: content-authoring
nav_id: content-authoring
category: Authoring
summary: Create a doc page and link it to a shelf with parent_shelf.
author: Vujca
date: 2025-12-04
---
### Steps
1. Create a file in `_docs/`, e.g. `_docs/deploy-on-ubuntu.md`.
2. Add front matter:
   ```yaml
   ---
   title: Deploy on Ubuntu
   parent_shelf: getting-started
   nav_id: getting-started
   category: Setup
   summary: Steps to deploy on Ubuntu with Nginx.
   tags: [ubuntu, nginx]
   ---
   ```
3. Write your Markdown content. The `doc` layout renders breadcrumbs and metadata automatically.

### Tips
- `parent_shelf` must match the shelf’s `shelf_id`.
- `nav_id` should also match so the sidebar highlights correctly.
- Use `date` if you want updated timestamps shown on cards.
