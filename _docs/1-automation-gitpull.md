---
title: Automating git pulls for content updates
parent_shelf: getting-started
project_id: wiki
nav_id: getting-started
category: Authoring
summary: Keep the wiki updated automatically from a Git remote.
author: Vujca
order: 5
date: 2025-12-04
---
### Bare metal / VM (systemd timer)
- Use the `wiki-refresh.timer` example from the bare-metal guide.
- Schedule hourly or every 5 minutes depending on how often you publish.

### Cron alternative
```cron
*/10 * * * * cd /srv/wiki && git pull && JEKYLL_ENV=production bundle exec jekyll build
```

### Docker git-sync
- Use the `git-sync` sidecar in the Docker Compose example. It runs `git pull` on an interval and the Jekyll container serves from the shared volume.

### Webhooks
- For near-real-time updates, expose a small endpoint that runs `git pull && jekyll build` when GitHub/GitLab sends a push webhook.

### GitHub Pages
- Commits to the repository trigger rebuilds automatically. Use branch protection to keep `main` stable.
