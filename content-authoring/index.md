---
layout: default
title: Content authoring
nav_id: content-authoring
permalink: /content-authoring/
---
<nav aria-label="Breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="{{ '/' | relative_url }}">Home</a></li>
    <li class="breadcrumb-item active" aria-current="page">Content authoring</li>
  </ol>
</nav>
<section class="hero">
  <p class="text-uppercase text-muted mb-2" style="letter-spacing:3px;font-size:0.8rem;">Writing</p>
  <h2>Structure, write, and brand your docs</h2>
  <p>Use navigation data for top-level links, shelves for grouped topics, and doc pages for detailed articles. Styling lives in SCSS for easy theming.</p>
</section>
<section class="content-layout">
  <div class="shelf-card">
    <h3>1. Navigation and sections</h3>
    <ul>
      <li>Top navigation lives in <code>_data/navigation.yml</code> (id, title, URL, icon).</li>
      <li>Section meta (badge text, intro, hero CTA) lives in <code>_data/sections.yml</code> keyed by the same id.</li>
      <li>Each page should include <code>nav_id</code> in its front matter so the active state highlights correctly.</li>
      <li>To add a new nav item, add entries in both YAML files and create a page at the matching URL.</li>
    </ul>
  </div>
  <div class="shelf-card">
    <h3>2. Create sections</h3>
    <ol>
      <li>Create a folder with <code>index.md</code> (for example, <code>platform/index.md</code>).</li>
      <li>Front matter example:
        <pre><code>---
layout: default
title: Platform
nav_id: platform
permalink: /platform/
---</code></pre>
      </li>
      <li>Use the <code>section</code> layout if you prefer a landing page that lists shelves automatically.</li>
    </ol>
  </div>
  <div class="shelf-card">
    <h3>3. Shelves</h3>
    <ul>
      <li>Shelves live in <code>_shelves/</code>. Each Markdown file represents a shelf (topic hub).</li>
      <li>Front matter keys:
        <ul>
          <li><code>section</code>: matches the section id (e.g., <code>getting-started</code>).</li>
          <li><code>shelf_id</code>: slug used to attach docs.</li>
          <li><code>title</code>, <code>summary</code>, optional <code>category</code>, <code>date</code>, <code>author</code>, <code>read_time</code>.</li>
        </ul>
      </li>
      <li>Use the <code>shelf</code> layout so linked docs appear automatically beneath it.</li>
    </ul>
  </div>
  <div class="shelf-card">
    <h3>4. Add a detailed doc beneath a shelf</h3>
    <ol>
      <li>Create a file in <code>_docs/</code> such as <code>deploying-on-ubuntu.md</code>.</li>
      <li>Front matter keys:
        <ul>
          <li><code>parent_shelf</code>: the <code>shelf_id</code> to nest under.</li>
          <li><code>section</code>: same id as the shelf’s section.</li>
          <li>Optional: <code>summary</code>, <code>category</code>, <code>tags</code>, <code>date</code>, <code>author</code>, <code>read_time</code>.</li>
        </ul>
      </li>
      <li>Use standard Markdown. The <code>doc</code> layout renders breadcrumbs and metadata.</li>
    </ol>
  </div>
  <div class="shelf-card">
    <h3>5. Styling (colors, logo, typography)</h3>
    <ul>
      <li>SCSS entry point: <code>_scss/main.scss</code>. Variables live in <code>_scss/_variables.scss</code> (primary color, backgrounds, border radii, shadows).</li>
      <li>Layout tweaks: <code>_scss/_layout.scss</code> (sidebar width, content spacing) and <code>_scss/_components.scss</code> (cards, buttons, badges).</li>
      <li>Typography and prose: <code>_scss/_prose.scss</code>. Fonts are loaded in <code>_layouts/default.html</code>; swap the Google Fonts URL if you prefer a different family.</li>
      <li>Logos and favicons: replace <code>favicon.ico</code>, <code>favicon.png</code>, and update the <code>.logo-section</code> styles if you change sizing.</li>
      <li>Run <code>bundle exec jekyll build</code> to regenerate compiled CSS in <code>assets/css/style.css</code> when changing SCSS.</li>
    </ul>
  </div>
  <div class="shelf-card">
    <h3>6. Automating git pulls for content updates</h3>
    <ul>
      <li>Server or VM: use a cron job or systemd timer to <code>git pull</code> and rebuild on a schedule.</li>
      <li>Docker: use the <code>git-sync</code> sidecar in the Compose example from Getting started.</li>
      <li>GitHub Pages: commits trigger rebuilds automatically. Consider enabling branch protection to keep the main branch healthy.</li>
      <li>Set up a webhook (GitHub/GitLab) to hit a small pull-and-build script on your server for near-real-time updates.</li>
    </ul>
  </div>
</section>
