# TomeksDEV Wiki

Bookstack-inspired wiki powered by Jekyll. Content is grouped into “shelves” such as Architecture, Project DOC, or Snippets; each shelf can expose deeper documentation cards and breadcrumbs automatically.

## Features

- Persistent left sidebar navigation rendered from `_data/navigation.yml`.
- Shelves and docs stored as separate collections (`_shelves`, `_docs`) for clean authoring.
- Modular SCSS stack in `_scss/` compiled to `assets/css/style.css`.
- Bootstrap 5.3 + Font Awesome 6.4 delivered locally (no CDN dependency).
- Ready-to-run on macOS/Linux, Docker Compose, or GitHub Pages.

## Repository layout

- `_layouts/default.html` – base layout with sidebar + typography.
- `_layouts/section.html` – lists shelves for Architecture, Project DOC, etc.
- `_layouts/shelf.html` – shelf detail page; automatically lists child docs.
- `_layouts/doc.html` – deep dive documentation layout.
- `_data/navigation.yml` – sidebar links and icons.
- `_data/sections.yml` – hero copy and badges per section.
- `_shelves/*.md` – main shelf entries (`section`, `shelf_id`, metadata).
- `_docs/*.md` – documentation cards referenced by `parent_shelf`.
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

## Content authoring

### Adding a new shelf

1. Create `_shelves/my-topic.md`.
2. Fill the front matter:

   ```yaml
   ---
   title: My Topic
   section: architecture   # architecture, project-doc, snippets, etc.
   shelf_id: my-topic      # unique slug for linking docs
   summary: Short description
   category: Infrastructure
   author: Vujca
   read_time: 5
   date: 2025-05-01
   ---
   ```

3. Write Markdown content below the front matter. The shelf appears automatically on the corresponding section page.

### Adding a detailed doc beneath a shelf

1. Ensure the parent shelf defines `shelf_id`.
2. Create `_docs/my-topic-deployment.md`:

   ```yaml
   ---
   title: Deployment Checklist
   section: architecture
   parent_shelf: my-topic   # matches shelf_id
   summary: Step-by-step deployment details.
   category: Runbook
   author: Platform Team
   read_time: 7
   date: 2025-05-05
   ---
   ```

3. The shelf page shows a card for every doc with matching `parent_shelf`.

### Navigation & sections

- Update `_data/navigation.yml` to add sidebar entries (id/title/url/icon).
- Extend `_data/sections.yml` for hero text/badges tied to nav IDs.

## Styling

- All SCSS lives in `_scss/` partials and is composed via `_scss/main.scss`.
- `assets/css/style.scss` has YAML front matter so Jekyll compiles it.
- Fonts/Bootstrap/FontAwesome are vendored; update files inside `assets/vendor/*` if you upgrade versions.

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
version: "3.9"
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
