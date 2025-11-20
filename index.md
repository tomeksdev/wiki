---
layout: default
title: Home
nav_id: home
permalink: /
---
<section class="hero">
  <h1>Hey there — welcome to the TomeksDEV Wiki</h1>
  <p>Think of this as your backstage pass to how everything runs:</p>
  <ul>
    <li>💾 <strong>Infrastructure setups</strong></li>
    <li>🧠 <strong>Architecture decisions</strong></li>
    <li>🛠️ <strong>Project insights &amp; docs</strong></li>
  </ul>
  <p>Grab what you need, when you need it.</p>
</section>
{% assign latest_docs = site.docs | sort: "date" | reverse %}
{% if latest_docs.size > 0 %}
<section class="content-layout" style="margin-bottom:2rem;">
  <h2 style="font-weight:700;">Latest documentation</h2>
  <div class="shelf-grid">
    {% for doc in latest_docs limit:4 %}
      <a class="shelf-card" href="{{ doc.url | relative_url }}">
        <div class="meta">{{ doc.category | default: 'Doc' }} · {{ doc.date | date: "%b %d, %Y" }}</div>
        <h3>{{ doc.title }}</h3>
        <p>{{ doc.summary | default: doc.excerpt | strip_html | truncate: 140 }}</p>
        <div class="meta">Author: {{ doc.author | default: 'Unknown' }}{% if doc.read_time %} · {{ doc.read_time }} min read{% endif %}</div>
      </a>
    {% endfor %}
  </div>
</section>
{% endif %}
<section class="content-layout">
  <div class="shelf-grid">
    {% for item in site.data.navigation %}
      {% unless item.id == 'home' %}
        {% assign section_data = site.data.sections[item.id] %}
        <a class="shelf-card" href="{{ item.url | relative_url }}">
          <div class="meta">{{ section_data.badge | default: 'Section' }}</div>
          <h3>{{ item.title }}</h3>
          <p>{{ section_data.intro | default: 'Dive into this shelf to start documenting.' }}</p>
        </a>
      {% endunless %}
    {% endfor %}
  </div>
</section>
