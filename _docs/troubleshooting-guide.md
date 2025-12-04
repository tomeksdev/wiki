---
title: Troubleshooting guide
parent_shelf: troubleshooting
nav_id: troubleshooting
category: Support
summary: Fix common build failures, asset issues, and deployment problems.
author: Vujca
date: 2025-12-04
---
### Build errors
- Run `bundle exec jekyll build --trace` to see the full stack trace.
- Ensure Ruby headers and build tools are installed (`build-essential` or `@development-tools`).
- Delete `.jekyll-cache` and `_site` then rebuild.
- If Bundler versions differ: `gem install bundler` then `bundle update --bundler`.

### Assets not loading
- Set `url` and `baseurl` in `_config.yml` when hosting under a subpath (e.g., project sites on GitHub Pages).
- Confirm `assets/` exists in the deployed output and your web server points to `_site`.
- Hard refresh the browser to clear stale caches.
- Source map 404s are harmless—remove `/*# sourceMappingURL=... */` comments if you want silence.

### Local server issues
- Port conflict: `bundle exec jekyll serve -P 4001`.
- LiveReload: ensure HTTP (not HTTPS) and no proxy blocks WebSocket connections.
- Drafts hidden: add `--drafts` to the serve command.

### Deployment problems
- GitHub Pages: check **Settings → Pages → Build logs**; remove unsupported plugins.
- Docker: ensure the git-sync container has network access to the remote repo (SSH keys or HTTPS creds).
- Custom domain SSL: verify DNS `A`/`CNAME` records and reissue certificates on your reverse proxy.
- Permissions: web server user must read `_site`.

### Content & navigation
- Sidebar not highlighting: `nav_id` on a doc should match its shelf `shelf_id`.
- Doc missing from shelf: `parent_shelf` must match the shelf’s `shelf_id`.
- Breadcrumbs: make sure the shelf exists and `parent_shelf` is set.
