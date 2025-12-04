---
layout: default
title: Home
nav_id: home
permalink: /
---
<section class="hero">
  <h1>TomeksDEV Wiki</h1>
  <p>A small, self-hostable wiki built with Jekyll. Install it anywhere, sync it from Git, and keep your docs organized with shelves and pages.</p>
  <div class="d-flex flex-wrap gap-3 mt-2">
    <a class="btn btn-primary" href="{{ '/shelves/getting-started/' | relative_url }}">Install the wiki</a>
    <a class="btn btn-outline-light" href="{{ '/shelves/content-authoring/' | relative_url }}">Write &amp; style docs</a>
  </div>
</section>
{% assign shelves_nav = site.shelves | sort: "order" %}
{% if shelves_nav.size > 0 %}
<section class="content-layout" style="margin-bottom:2rem;">
  <h2 style="font-weight:700;">Browse shelves</h2>
  <div class="shelf-grid">
    {% for shelf in shelves_nav %}
      <a class="shelf-card" href="{{ shelf.url | relative_url }}">
        <div class="meta">{{ shelf.category | default: 'Shelf' }}{% if shelf.date %} · Updated {{ shelf.date | date: "%b %d, %Y" }}{% endif %}</div>
        <h3>{{ shelf.title }}</h3>
        <p>{{ shelf.summary | default: shelf.excerpt | strip_html | truncate: 140 }}</p>
        <div class="meta">Maintained by {{ shelf.author | default: 'Wiki Team' }}</div>
      </a>
    {% endfor %}
  </div>
</section>
{% endif %}
