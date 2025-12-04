---
layout: default
title: Introduction
nav_id: home
permalink: /
---
<section class="hero">
  <h1>TomeksDEV Wiki</h1>
  <p>A self-hostable Jekyll wiki template. Install it locally, run it on a server, or publish it with GitHub Pages and keep content synced from Git.</p>
  <div class="d-flex flex-wrap gap-3">
    <a class="btn btn-primary" href="{{ '/getting-started/' | relative_url }}">Install the wiki</a>
    <a class="btn btn-outline-light" href="{{ '/content-authoring/' | relative_url }}">Write and style docs</a>
  </div>
</section>
<section class="content-layout">
  <div class="shelf-grid">
    {% for item in site.data.navigation %}
      {% unless item.id == 'home' %}
        {% assign section_data = site.data.sections[item.id] %}
        <a class="shelf-card" href="{{ item.url | relative_url }}">
          <div class="meta">{{ section_data.badge | default: 'Section' }}</div>
          <h3>{{ item.title }}</h3>
          <p>{{ section_data.intro | default: 'Start here to explore this topic.' }}</p>
        </a>
      {% endunless %}
    {% endfor %}
  </div>
</section>
<section class="content-layout">
  <div class="shelf-card">
    <h3>What you get</h3>
    <ul>
      <li>Multiple deployment paths: local dev, bare-metal hosting, Docker, or GitHub Pages.</li>
      <li>Structured authoring with navigation, sections, shelves, and doc pages.</li>
      <li>Branding knobs: colors, logo, fonts, and layout tweaks via SCSS.</li>
      <li>Automation patterns to keep content synced from any Git remote.</li>
    </ul>
  </div>
</section>
