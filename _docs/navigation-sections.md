---
title: Navigation & sections
parent_shelf: content-authoring
nav_id: content-authoring
category: Authoring
summary: How the sidebar is built and how to control the order of items.
author: Vujca
date: 2025-12-04
---
### How the sidebar works
- **Home** is the only static entry.
- All other entries come from the `_shelves/` collection. Each shelf has `shelf_id`, `nav_id`, `nav_title`, `nav_icon`, and `order` front matter.
- **Contact** stays a static page at `/contact/` and is appended after the shelves.

### Ordering
Use the `order` key on shelves to sort them. Lower numbers appear first.

```yaml
---
title: Getting started
shelf_id: getting-started
nav_id: getting-started
order: 2
---
```

### Renaming items
- Change `nav_title` or `title` in the shelf file to update the sidebar label.
- Update `nav_icon` with any Font Awesome icon class (e.g., `fa-solid fa-rocket`).

### Sections?
This template uses shelves for navigation rather than a separate “section” collection. If you prefer top-level pages, create a regular page and give it a `nav_id`, but shelves are the recommended pattern.
