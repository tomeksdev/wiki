---
title: Single-project vs multi-project
parent_shelf: content-authoring
project_id: wiki
category: Navigation
summary: Configure whether the wiki sidebar shows shelves or projects, how ordering works, and how to add or migrate projects.
author: Vujca
order: 1
date: 2025-12-16
---
You can flip the wiki between **single-project** (original behavior) and **multi-project** modes from `_config.yml`. Multi-project keeps each project isolated with its own shelves and docs; single-project keeps the original shelf-only navigation.

## Switch modes
- Single-project: set `project_mode: single` and `default_project_id: <project>`. The sidebar lists shelves for the chosen project (default: `wiki`).
- Multi-project: set `project_mode: multi`. The sidebar lists every project in `_projects/`. Clicking a project opens its shelves and docs, and the sidebar keeps that project highlighted while you browse shelves/docs inside it.

## Add a project
1) Create a file in `_projects/`:
   ```yaml
   ---
   title: Awesome App
   project_id: awesome-app
   nav_id: awesome-app
   nav_title: Awesome App
   nav_icon: fa-solid fa-folder
   order: 3
   ---
   Short description…
   ```
2) Add shelves to `_shelves/` with `project_id: awesome-app`. Example:
   ```yaml
   ---
   title: Getting Started
   shelf_id: awesome-getting-started
   parent_shelf: # leave blank
   project_id: awesome-app
   order: 1
   ---
   ```
3) Add docs to `_docs/` with both `parent_shelf` and `project_id` set:
   ```yaml
   ---
   title: Install
   parent_shelf: awesome-getting-started
   project_id: awesome-app
   ---
   ```

## Navigation ordering (multi-project)
- The sidebar uses each project’s `order` value (from the file in `_projects/`) and prefixes the number before the name for clarity.
- If `order` is missing, the loop index is used (1, 2, 3…).
- Shelves continue to sort by their own `order` inside the project.
- In single-project mode the numeric prefix is hidden because the sidebar shows shelves, not projects.

## Keep the original wiki
- The existing template lives as the `TomeksDEV Wiki` project in `_projects/wiki.md`.
- All existing shelves/docs default to `project_id: wiki` via collection defaults in `_config.yml`.
- If you return to single-project mode, set `default_project_id: wiki` to show the original shelves.

## Example project
- `WireGuard Install with GUI` lives in `_projects/wireguard-install-with-gui.md` with its shelf `_shelves/wireguard-install.md` and doc `_docs/wireguard-readme.md`. Use it as a pattern for adding more projects.

## Migrate an existing single-project wiki to multi-project
1. Set `project_mode: multi` in `_config.yml`.
2. Add a project file for your current content (e.g., `_projects/wiki.md`) and make sure shelves/docs have either `project_id: wiki` in front matter or rely on the defaults already defined in `_config.yml`.
3. Add additional project files, shelves, and docs following the pattern above.
4. Serve locally (`bundle exec jekyll serve`) and confirm the sidebar shows numbered projects. Click into each to verify shelves and breadcrumbs stay scoped.
