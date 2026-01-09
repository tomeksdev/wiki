---
title: Bare-metal installation
parent_shelf: getting-started
project_id: wiki
nav_id: getting-started
category: Setup
summary: Build the site on a server and serve it with Nginx or Apache.
author: Vujca
order: 1
date: 2025-12-04
---
### 1) Prepare the host
- Create a non-root user with sudo.
- Install Ruby, Bundler, and build tools (same packages as the local install guide).

### 2) Deploy the repo
```bash
sudo mkdir -p /srv/wiki
sudo chown -R $USER:$USER /srv/wiki
git clone https://github.com/<you>/wiki.git /srv/wiki
cd /srv/wiki
bundle install
```

### 3) Build
```bash
JEKYLL_ENV=production bundle exec jekyll build
```
Static files land in `/srv/wiki/_site`.

### 4) Serve with Nginx
Example server block:
```nginx
server {
  listen 80;
  server_name docs.example.com;
  root /srv/wiki/_site;

  location /assets/ {
    expires 7d;
    add_header Cache-Control "public";
  }
}
```

### 5) Keep it updated (systemd timer)
`/etc/systemd/system/wiki-refresh.service`:
```ini
[Unit]
Description=Wiki git pull and rebuild

[Service]
Type=oneshot
WorkingDirectory=/srv/wiki
ExecStart=/usr/bin/git pull
ExecStart=/usr/bin/JEKYLL_ENV=production /usr/bin/bundle exec jekyll build
```
`/etc/systemd/system/wiki-refresh.timer`:
```ini
[Unit]
Description=Refresh wiki hourly

[Timer]
OnCalendar=hourly
Persistent=true

[Install]
WantedBy=timers.target
```
Enable with `sudo systemctl enable --now wiki-refresh.timer`.
