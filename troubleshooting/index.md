---
layout: default
title: Troubleshooting
nav_id: troubleshooting
permalink: /troubleshooting/
---
<nav aria-label="Breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="{{ '/' | relative_url }}">Home</a></li>
    <li class="breadcrumb-item active" aria-current="page">Troubleshooting</li>
  </ol>
</nav>
<section class="hero">
  <p class="text-uppercase text-muted mb-2" style="letter-spacing:3px;font-size:0.8rem;">Support</p>
  <h2>Fix common build, asset, and deployment issues</h2>
  <p>Use these checks before opening an issue. Most problems come from missing gems, base URL settings, or stale caches.</p>
</section>
<section class="content-layout">
  <div class="shelf-card">
    <h3>Build fails or gems missing</h3>
    <ul>
      <li>Run <code>bundle exec jekyll build --trace</code> to see the stack trace.</li>
      <li>Ensure Ruby headers and make tools are installed (<code>build-essential</code> / <code>@development-tools</code>).</li>
      <li>Delete <code>.jekyll-cache</code> and <code>_site</code> then rebuild.</li>
      <li>If Bundler version mismatches, run <code>gem install bundler</code> then <code>bundle update --bundler</code>.</li>
    </ul>
  </div>
  <div class="shelf-card">
    <h3>Assets not loading (CSS/JS/fonts)</h3>
    <ul>
      <li>Set <code>url</code> and <code>baseurl</code> in <code>_config.yml</code> when hosting under a subpath (e.g., GitHub Pages project site).</li>
      <li>Confirm <code>assets/</code> exists in the deployed output. On bare metal, check your web server root points to <code>_site</code>.</li>
      <li>Clear browser cache or do a hard refresh to avoid stale assets.</li>
      <li>Source map 404s are safe to ignore; remove <code>/*# sourceMappingURL=... */</code> comments if you want silence in devtools.</li>
    </ul>
  </div>
  <div class="shelf-card">
    <h3>Local dev server issues</h3>
    <ul>
      <li>Port already in use: run <code>bundle exec jekyll serve -P 4001</code> to use a different port.</li>
      <li>LiveReload not working: ensure you are on HTTP (not HTTPS) and no proxy strips WebSocket connections.</li>
      <li>Drafts not visible: add <code>--drafts</code> to the serve command.</li>
    </ul>
  </div>
  <div class="shelf-card">
    <h3>Deployment problems</h3>
    <ul>
      <li>GitHub Pages build errors: check <strong>Settings → Pages → Build logs</strong> and remove unsupported plugins.</li>
      <li>Docker site not updating: make sure the git-sync container can reach the remote and has SSH/HTTPS access.</li>
      <li>SSL/cert issues on custom domains: verify DNS <code>A</code>/<code>CNAME</code> records and reissue certificates on your reverse proxy.</li>
      <li>Permissions on bare metal: ensure the web server user can read the <code>_site</code> directory.</li>
    </ul>
  </div>
  <div class="shelf-card">
    <h3>Content and navigation</h3>
    <ul>
      <li>Nav item not highlighted: check <code>nav_id</code> matches the id in <code>_data/navigation.yml</code>.</li>
      <li>Docs not appearing under shelves: ensure <code>parent_shelf</code> on the doc matches the <code>shelf_id</code> on the shelf file.</li>
      <li>Broken breadcrumbs: set <code>section</code> on both shelves and docs.</li>
    </ul>
  </div>
</section>
