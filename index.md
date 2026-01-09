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
    <a class="btn btn-danger" style="background: var(--color-accent);" href="{{ '/shelves/getting-started/' | relative_url }}">Install the wiki</a>
    <a class="btn btn-outline-light" href="{{ '/shelves/content-authoring/' | relative_url }}">Write &amp; style docs</a>
  </div>
</section>
{% assign project_mode = site.project_mode | default: 'single' %}
{% assign default_project_id = site.default_project_id | default: 'wiki' %}
{% assign home_project_id = page.project_id | default: default_project_id %}

{% if project_mode == 'single' %}
  {% assign latest_docs = site.docs | where: "project_id", home_project_id | sort: "date" | reverse %}
{% else %}
  {% assign latest_docs = site.docs | sort: "date" | reverse %}
{% endif %}
{% if latest_docs.size > 0 %}
<section class="content-layout" style="margin-bottom:2rem;">
  <h2 style="font-weight:700;">Latest documentation</h2>
  <div class="shelf-grid">
    {% for doc in latest_docs limit:6 %}
      <a class="shelf-card" href="{{ doc.url | relative_url }}">
        <div class="meta">
          {% if project_mode == 'multi' %}
            {% assign project_page = site.projects | where: "project_id", doc.project_id | first %}
            {{ project_page.nav_title | default: project_page.title | default: doc.project_id | default: 'Project' }} ·
          {% endif %}
          {{ doc.category | default: 'Doc' }}{% if doc.date %} · Updated {{ doc.date | date: "%b %d, %Y" }}{% endif %}
        </div>
        <h3>{{ doc.title }}</h3>
        <p>{{ doc.summary | default: doc.excerpt | strip_html | truncate: 140 }}</p>
        <div class="meta">Maintained by {{ doc.author | default: 'Wiki Team' }}</div>
      </a>
    {% endfor %}
  </div>
</section>
{% endif %}
