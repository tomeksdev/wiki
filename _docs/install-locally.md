---
title: Install locally (Debian/Ubuntu/Fedora/CentOS/RHEL/macOS)
parent_shelf: getting-started
nav_id: getting-started
category: Setup
summary: Install Ruby, Bundler, and Jekyll on your workstation to develop and preview the wiki.
author: Vujca
date: 2025-12-04
---
### 1) Install dependencies
- **Debian/Ubuntu**: `sudo apt update && sudo apt install ruby-full build-essential zlib1g-dev git`
- **Fedora**: `sudo dnf install ruby ruby-devel @development-tools redhat-rpm-config git`
- **CentOS/RHEL 9+**: `sudo dnf install ruby ruby-devel @development-tools redhat-rpm-config git`
- **macOS (Homebrew)**: `brew install ruby git` and add `export PATH="/opt/homebrew/opt/ruby/bin:$PATH"` to your shell profile.

### 2) Clone and install gems
```bash
git clone https://github.com/<you>/wiki.git
cd wiki
bundle install
```

### 3) Run locally
- Preview with drafts and livereload: `bundle exec jekyll serve --livereload --drafts`
- Open `http://localhost:4000`

### 4) Production build
```bash
JEKYLL_ENV=production bundle exec jekyll build
```
Outputs the static site to `_site/`.
