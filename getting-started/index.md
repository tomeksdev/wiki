---
layout: default
title: Getting started
nav_id: getting-started
permalink: /getting-started/
---
<nav aria-label="Breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="{{ '/' | relative_url }}">Home</a></li>
    <li class="breadcrumb-item active" aria-current="page">Getting started</li>
  </ol>
</nav>
<section class="hero">
  <p class="text-uppercase text-muted mb-2" style="letter-spacing:3px;font-size:0.8rem;">Setup</p>
  <h2>Install and publish the wiki</h2>
  <p>Choose the path that fits your environment: local workstation, bare-metal server, Docker, or GitHub Pages.</p>
</section>
<section class="content-layout">
  <div class="shelf-card">
    <h3>1. Install locally (Debian, Ubuntu, Fedora, CentOS, RHEL, macOS)</h3>
    <ol>
      <li>Install Ruby 3.x, Bundler, and build tools.
        <ul>
          <li>Debian/Ubuntu: <code>sudo apt update && sudo apt install ruby-full build-essential zlib1g-dev git</code></li>
          <li>Fedora: <code>sudo dnf install ruby ruby-devel @development-tools redhat-rpm-config git</code></li>
          <li>CentOS/RHEL (9+): <code>sudo dnf install ruby ruby-devel @development-tools redhat-rpm-config git</code></li>
          <li>macOS (Homebrew): <code>brew install ruby git</code> then ensure <code>export PATH=\"/opt/homebrew/opt/ruby/bin:$PATH\"</code>.</li>
        </ul>
      </li>
      <li>Clone the repository: <code>git clone https://github.com/&lt;you&gt;/wiki.git && cd wiki</code>.</li>
      <li>Install gems: <code>bundle install</code>.</li>
      <li>Run a dev server: <code>bundle exec jekyll serve --livereload --drafts</code> (visit <code>http://localhost:4000</code>).</li>
      <li>Production build: <code>JEKYLL_ENV=production bundle exec jekyll build</code> outputs to <code>_site</code>.</li>
    </ol>
  </div>
  <div class="shelf-card">
    <h3>2. Bare-metal installation</h3>
    <ol>
      <li>Create a non-root user with sudo and install the same Ruby toolchain as above.</li>
      <li>Clone the wiki to <code>/srv/wiki</code> (or another path) and run <code>bundle install</code>.</li>
      <li>Build the site to <code>/srv/wiki/_site</code>: <code>JEKYLL_ENV=production bundle exec jekyll build</code>.</li>
      <li>Serve the static site with Nginx or Apache:
        <ul>
          <li>Point <code>root</code> (Nginx) or <code>DocumentRoot</code> (Apache) to <code>_site</code>.</li>
          <li>Enable HTTP caching for <code>/assets</code> and add gzip/brotli if available.</li>
        </ul>
      </li>
      <li>Keep content updated with a simple systemd timer:
        <pre><code>[Unit]
Description=Wiki git pull

[Service]
Type=oneshot
WorkingDirectory=/srv/wiki
ExecStart=/usr/bin/git pull
ExecStart=/usr/bin/JEKYLL_ENV=production /usr/bin/bundle exec jekyll build

[Install]
WantedBy=multi-user.target</code></pre>
        <p>Create a matching <code>.timer</code> that runs every 5 minutes or hourly.</p>
      </li>
    </ol>
  </div>
  <div class="shelf-card">
    <h3>3. Docker installation with automated git pulls</h3>
    <p>Use Docker Compose to keep the repo synced and serve the site.</p>
    <pre><code class="language-yaml">services:
  git-sync:
    image: alpine/git
    volumes:
      - wiki-data:/site
    entrypoint: /bin/sh -c "
      if [ ! -d /site/.git ]; then git clone https://github.com/&lt;you&gt;/wiki.git /site; fi;
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
  wiki-data: {}</code></pre>
    <p>Replace the repository URL, then run <code>docker compose up -d</code>. Jekyll serves from the synced volume, and git pulls every 5 minutes.</p>
  </div>
  <div class="shelf-card">
    <h3>4. GitHub Pages deployment</h3>
    <ol>
      <li>Push the repository to GitHub with the <code>CNAME</code> file updated (if using a custom domain).</li>
      <li>In <strong>Settings → Pages</strong>, select the <code>main</code> branch and <code>/</code> (root) for the site folder.</li>
      <li>Set <code>baseurl</code> (e.g., <code>/wiki</code>) and <code>url</code> (e.g., <code>https://username.github.io</code>) in <code>_config.yml</code> if serving from a subpath.</li>
      <li>Commit and push; GitHub Pages builds automatically. If you need plugins not allowed by GitHub, push the built <code>_site</code> to a <code>gh-pages</code> branch instead.</li>
      <li>Enable HTTPS and add DNS records if using a custom domain; ensure the <code>CNAME</code> file matches.</li>
    </ol>
  </div>
</section>
