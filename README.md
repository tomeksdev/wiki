# TomeksDEV Wiki

Bookstack-inspired wiki powered by Jekyll. Content is grouped into projects (optional) and “shelves”; each shelf can expose deeper documentation cards and breadcrumbs automatically.

![GitHub release](https://img.shields.io/badge/release-v1.1.0-darkgreen)

[![pages-build-deployment](https://github.com/tomeksdev/wiki/actions/workflows/pages/pages-build-deployment/badge.svg)](https://github.com/tomeksdev/wiki/actions/workflows/pages/pages-build-deployment) [![CodeQL Advanced](https://github.com/tomeksdev/wiki/actions/workflows/codeql.yml/badge.svg)](https://github.com/tomeksdev/wiki/actions/workflows/codeql.yml) [![Bundler Audit](https://github.com/tomeksdev/wiki/actions/workflows/bundler-audit.yml/badge.svg)](https://github.com/tomeksdev/wiki/actions/workflows/bundler-audit.yml) [![Scorecard supply-chain security](https://github.com/tomeksdev/wiki/actions/workflows/scorecard.yml/badge.svg)](https://github.com/tomeksdev/wiki/actions/workflows/scorecard.yml)

## Features

- Switchable **single-project** (shelves-only) or **multi-project** navigation (`project_mode` in `_config.yml`).
- Sidebar highlights the active project while browsing shelves/docs in multi-project mode and prefixes project names with their `order`.
- Projects, shelves, and docs stored as separate collections (`_projects`, `_shelves`, `_docs`) for clean authoring and scoping.
- Modular SCSS stack in `_scss/` compiled to `assets/css/style.css`.
- Bootstrap 5.3 + Font Awesome 6.4 delivered locally (no CDN dependency).
- Ready-to-run on macOS/Linux, Docker Compose, or GitHub Pages.

## Repository layout

- `_layouts/default.html` – base layout with sidebar + theme toggles.
- `_layouts/project.html` – project landing; lists shelves within a project.
- `_layouts/shelf.html` – shelf detail page; automatically lists child docs for that project.
- `_layouts/doc.html` – deep dive documentation layout with breadcrumbs to project/shelf.
- `_projects/*.md` – project entries (`project_id`, `order`, nav metadata).
- `_shelves/*.md` – shelf entries (`project_id`, `shelf_id`, metadata).
- `_docs/*.md` – documentation cards (`project_id`, `parent_shelf`).
- `_data/navigation.yml` – global links (Home/Contact); stays short on purpose.
- `_data/sections.yml` – hero copy and badges per section (optional legacy use).
- `_scss/*` + `assets/css/style.scss` – SCSS partials & build entry.
- `assets/vendor/bootstrap/*`, `assets/vendor/fontawesome/*` – vendored CSS/fonts.
- `template_home.html` – static design reference (excluded from builds).

## Prerequisites

- Ruby 3.0+ with Bundler (`gem install bundler`).
- GCC/Make build tools (needed for native gems).
- Node.js is **not** required; Jekyll handles asset compilation.

### Installing prerequisites on Debian/Ubuntu

```bash
sudo apt update
sudo apt install -y ruby-full build-essential zlib1g-dev
echo '# Ruby gems to ~/.gem' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
gem install bundler
```

### On Fedora/CentOS/RHEL

```bash
sudo dnf install ruby ruby-devel gcc make
gem install bundler
```

### On macOS

```bash
brew install ruby
gem install bundler
```

## Local development workflow

```bash
git clone https://github.com/<you>/wiki.git
cd wiki
bundle install
bundle exec jekyll serve --livereload
```

Visit <http://localhost:4000>. Live reload refreshes as you edit shelves/docs.

## Single-project vs multi-project

You can run the wiki as a single project (original behavior) or as multiple projects side by side. Switch modes in `_config.yml`:

- `project_mode: single` and `default_project_id: wiki` (or your preferred ID) show shelves for only that project in the sidebar.
- `project_mode: multi` lists every project in `_projects/` in the sidebar. Clicking a project keeps it highlighted while you browse its shelves and docs.
- Project ordering: set `order` in each `_projects/*.md` file to control sidebar order; the order number is prefixed before the project name in multi-project mode. In single-project mode the sidebar shows shelves, so the prefix is hidden.

### Example front matter (projects)

```yaml
---
title: WireGuard Install with GUI
project_id: wireguard-gui
nav_id: wireguard-gui         # used for active state; usually matches project_id
nav_title: WireGuard GUI Installer
nav_icon: fa-solid fa-lock
order: 2                      # controls sidebar order in multi-project mode
summary: Documentation for the WireGuard GUI installer.
category: Networking
author: TomeksDEV
---
```

### How the menu behaves
- Single-project: sidebar shows shelves for `default_project_id` only. Use each shelf’s `order` to sort.
- Multi-project: sidebar shows projects with numeric prefixes from `order`. Inside a project, shelves still sort by their own `order`. Breadcrumbs show Home → Project → Shelf/Doc.

### Naming for easier maintenance
- For multi-project setups, consider prefixing filenames in `_projects/`, `_shelves/`, and `_docs/` with a two-digit order to keep them grouped when browsing the repo. Example: `_projects/01-wiki.md`, `_projects/02-wireguard-gui.md`; `_shelves/01-getting-started.md`; `_docs/01-install.md`.
- The `order` front matter still controls display order; the numeric filename is just for your convenience.

### Example project wiring
- `_projects/wireguard-install-with-gui.md` → `_shelves/wireguard-install.md` → `_docs/wireguard-readme.md` shows a second project that lives beside the original `_projects/wiki.md`.

## Content authoring

### Adding a new shelf

1. Create `_shelves/my-topic.md`.
2. Fill the front matter (all commonly used fields shown):

   ```yaml
   ---
   title: My Topic
   project_id: wiki            # project this shelf belongs to
   shelf_id: my-topic          # unique slug; docs refer to this
   nav_id: my-topic            # used for active state; usually same as shelf_id
   nav_title: My Topic         # sidebar label (single-project mode)
   nav_icon: fa-solid fa-book  # optional Font Awesome icon
   summary: Short description
   category: Infrastructure
   order: 1                    # controls shelf order inside the project
   author: Vujca
   read_time: 5
   date: 2025-05-01
   nav_hidden: false           # set true to hide from sidebar if needed
   ---
   ```

3. Write Markdown content below the front matter. The shelf appears automatically inside its project and (in single-project mode) in the sidebar.

### Adding a detailed doc beneath a shelf

1. Ensure the parent shelf defines `shelf_id`.
2. Create `_docs/my-topic-deployment.md`:

   ```yaml
   ---
   title: Deployment Checklist
   project_id: wiki            # same project as the shelf
   parent_shelf: my-topic      # matches shelf_id
   nav_id: my-topic-deploy     # optional; for active state if needed
    order: 1                    # controls display order within the shelf
   summary: Step-by-step deployment details.
   category: Runbook
   author: Platform Team
   read_time: 7
   date: 2025-05-05
   nav_hidden: false
   ---
   ```

3. The shelf page shows a card for every doc with matching `parent_shelf` within the same `project_id`, ordered by `order`.

### Adding another project (multi-project mode)

1. Create `_projects/my-app.md` with `project_id`, `nav_title`, `order`, optional `nav_icon`, and a short description.
2. Add shelves in `_shelves/` that set `project_id: my-app` and unique `shelf_id` values.
3. Add docs in `_docs/` that set both `project_id: my-app` and `parent_shelf: <shelf_id>`.
4. Switch `project_mode: multi` in `_config.yml` (or stay in single mode and set `default_project_id: my-app` if you want only that project).

### Navigation & sections

- Sidebar behavior comes from `_layouts/default.html`. Home and Contact are hard-coded there; shelves or projects are injected dynamically based on `project_mode`.
- `_data/navigation.yml` is intended for static nav items if you want more links; wire them into `_layouts/default.html` if you need additional global links.
- `_data/sections.yml` is only used by the legacy `section` layout. For multi-project mode you do not need it. For single-project mode you typically rely on shelves instead of sections; keep it only if you create section pages using `_layouts/section.html`.

## Styling

- All SCSS lives in `_scss/` partials and is composed via `_scss/main.scss`, compiled to `assets/css/style.css` by Jekyll.
- Colors and typography: tweak `_scss/_variables.scss` (`--color-accent` for your red, `--color-bg`, `--color-text`, etc.).
- Layout and components: `_scss/_layout.scss` and `_scss/_components.scss`.
- Typography/content rendering (links, images, code blocks): `_scss/_prose.scss`.
- `assets/css/style.scss` only imports `@use "main";` with front matter so Jekyll builds the stylesheet.
- Vendored assets live in `assets/vendor/bootstrap/*` and `assets/vendor/fontawesome/*`; replace them if you upgrade versions.

## GitHub Pages deployment

1. Push the repo to GitHub.
2. Create `.github/workflows/jekyll.yml` (sample):

   ```yaml
   name: Build wiki
   on:
     push:
       branches: [ main ]
   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         - uses: ruby/setup-ruby@v1
           with:
             ruby-version: '3.3'
             bundler-cache: true
         - run: bundle exec jekyll build --baseurl ""
         - uses: actions/upload-pages-artifact@v3
           with:
             path: _site
     deploy:
       needs: build
       permissions:
         pages: write
         id-token: write
       environment:
         name: github-pages
         url: ${{ steps.deployment.outputs.page_url }}
       runs-on: ubuntu-latest
       steps:
         - id: deployment
           uses: actions/deploy-pages@v4
   ```

3. Enable GitHub Pages (Settings → Pages → Deploy from GitHub Actions).

## Docker Compose deployment

Use Docker when you want the wiki on your own server without installing Ruby:

```yaml
services:
  wiki:
    image: ghcr.io/jekyll/jekyll:4.3
    command: >
      bash -c "bundle install && jekyll serve --host 0.0.0.0 --port 4000 --watch"
    working_dir: /srv/wiki
    volumes:
      - .:/srv/wiki
    ports:
      - "4000:4000"
```

Start with `docker compose up --build`. The wiki is accessible at <http://localhost:4000>. For production, swap `jekyll serve` with `jekyll build` followed by an Nginx or Caddy container serving the generated `_site` directory.

## Bare-metal server (Ubuntu/Debian/other)

1. Install prerequisites (see above).
2. Create a dedicated user (optional):

   ```bash
   sudo adduser --system --group wiki
   sudo su - wiki
   ```

3. Clone repo, run `bundle install`, and build once:

   ```bash
   git clone https://github.com/<you>/wiki.git
   cd wiki
   bundle install
   bundle exec jekyll build
   ```

4. Serve `_site` with your web server of choice (Nginx example):

   ```nginx
   server {
     listen 80;
     server_name wiki.example.com;
     root /home/wiki/wiki/_site;
     location / {
       try_files $uri $uri/ =404;
     }
   }
   ```

Automate builds via cron or CI whenever you push updates.

## Troubleshooting

- **Sass errors** – ensure you’re using Dart Sass (`bundle exec jekyll build` already invokes it); partials rely on `@use` syntax.
- **Missing Bootstrap/Font Awesome** – confirm the files exist in `assets/vendor/*` and that `_layouts/default.html` references them.
- **No docs showing under a shelf** – verify the doc’s `parent_shelf` matches the shelf’s `shelf_id` and that `section` matches the parent section for breadcrumbs.

## License

Apache-2.0 License (see `LICENSE`). Feel free to adapt this wiki for your own infrastructure documentation.
