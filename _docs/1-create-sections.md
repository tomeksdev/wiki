---
title: Create sections (shelves)
parent_shelf: content-authoring
project_id: wiki
nav_id: content-authoring
category: Authoring
summary: Add or remove shelves to change the sidebar items.
author: Vujca
order: 2
date: 2025-12-04
---
Shelves act as “sections” in this template.

### Create a shelf
1. Add a file in `_shelves/`, e.g. `_shelves/platform.md`.
2. Use front matter:
   ```yaml
   ---
   title: Platform
   shelf_id: platform
   nav_id: platform
   nav_title: Platform
   nav_icon: fa-solid fa-layer-group
   order: 6
   summary: Docs about the platform stack.
   ---
   ```
3. Add Markdown content for the landing page body.

### Remove a shelf
- Delete the file from `_shelves/` and rebuild. The nav and shelf page disappear together.

### Hide a shelf from nav (optional)
- Add `nav_hidden: true` to the shelf if you want it accessible by URL but not listed.
