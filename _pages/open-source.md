---
layout: page
permalink: /open-source/
title: open source code
description: Code, datasets, and benchmarks released alongside our research.
nav: true
nav_order: 4
---

<!-- Content lives in _data/open_source.yml -->

<style>
  .oss-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 1rem;
  }
  .oss-grid .card-title {
    margin-bottom: 0.25rem;
  }
  .oss-repo {
    font-size: 0.85rem;
    opacity: 0.7;
    margin-bottom: 0.5rem;
  }
  .oss-links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
    margin-top: 0.75rem;
  }
</style>

<div class="oss-grid">
  {% for project in site.data.open_source %}
    <div class="card h-100">
      <div class="card-body">
        <h3 class="card-title">{{ project.title }}</h3>
        {% if project.venue %}<span class="badge">{{ project.venue }}</span>{% endif %}
        {% if project.repo %}
          <div class="oss-repo"><i class="fa-brands fa-github"></i> {{ project.repo }}</div>
        {% endif %}
        <p class="card-text">{{ project.description }}</p>
        <div class="oss-links">
          {% for link in project.links %}
            <a class="btn btn-sm" href="{{ link.url }}" target="_blank" rel="noopener noreferrer"><i class="{{ link.icon }}"></i> {{ link.label }}</a>
          {% endfor %}
          {% for paper in project.papers %}
            <a class="btn btn-sm" href="https://arxiv.org/abs/{{ paper.arxiv }}" target="_blank" rel="noopener noreferrer"
              ><i class="ai ai-arxiv"></i> {{ paper.label }}</a
            >
          {% endfor %}
        </div>
      </div>
    </div>
  {% endfor %}
</div>
