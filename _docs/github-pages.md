---
title: GitHub Pages deployment
parent_shelf: getting-started
nav_id: getting-started
category: Setup
summary: Publish the wiki with GitHub Pages using the main branch or a prebuilt site.
author: TomeksDEV
date: 2024-12-04
---
### 1) Repo setup
- Keep the `CNAME` file updated if you use a custom domain.
- Commit your changes to `main`.

### 2) Configure Pages
- In **Settings → Pages**, select the `main` branch and `/` (root) as the site folder.
- If your site lives under a subpath (project site), set `_config.yml`:
  - `url: https://username.github.io`
  - `baseurl: /your-repo-name`

### 3) Unsupported plugins?
GitHub Pages only allows whitelisted plugins. If you need others:
1. Build locally: `JEKYLL_ENV=production bundle exec jekyll build`.
2. Push the contents of `_site` to a `gh-pages` branch.
3. Point Pages to `gh-pages`.

### 4) Custom domains
- Add the domain in Pages settings and ensure the `CNAME` file matches.
- Add DNS records (CNAME for subdomains, A/AAAA for apex).
- Enable HTTPS after DNS propagates.
