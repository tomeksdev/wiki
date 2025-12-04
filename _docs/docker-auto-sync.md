---
title: Docker installation with automated git pull
parent_shelf: getting-started
nav_id: getting-started
category: Setup
summary: Run Jekyll in Docker and keep content synced from a Git remote.
author: TomeksDEV
date: 2024-12-04
---
Use a git-sync sidecar plus the official Jekyll image.

```yaml
services:
  git-sync:
    image: alpine/git
    volumes:
      - wiki-data:/site
    entrypoint: /bin/sh -c "
      if [ ! -d /site/.git ]; then git clone https://github.com/<you>/wiki.git /site; fi;
      cd /site;
      while true; do git pull && sleep 300; done"

  jekyll:
    image: jekyll/jekyll:4
    working_dir: /srv/jekyll
    command: jekyll serve --watch --host 0.0.0.0 --port 4000 --drafts
    volumes:
      - wiki-data:/srv/jekyll
    environment:
      JEKYLL_ENV: production
    ports:
      - "4000:4000"

volumes:
  wiki-data: {}
```

Steps:
1. Replace the repo URL with yours.
2. `docker compose up -d`.
3. Visit `http://localhost:4000`.

git-sync checks for changes every 5 minutes and Jekyll serves from the shared volume.
