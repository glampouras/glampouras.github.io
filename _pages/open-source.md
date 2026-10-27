---
layout: page
permalink: /open-source/
title: open source code
description: Code, datasets, and benchmarks released alongside our research.
nav: true
nav_order: 2
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
  .oss-wide {
    grid-column: 1 / -1;
  }
  .oss-subgrid {
    margin-top: 1rem;
  }
  .oss-sub {
    border: 1px solid var(--global-divider-color);
    border-radius: 0.5rem;
    padding: 0.75rem;
  }
  .oss-sub h4 {
    font-size: 1.05rem;
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
    <div class="card h-100{% if project.subprojects %} oss-wide{% endif %}">
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
        {% if project.subprojects %}
          <div class="oss-grid oss-subgrid">
            {% for sub in project.subprojects %}
              <div class="oss-sub">
                <h4>{{ sub.title }}</h4>
                {% if sub.venue %}<span class="badge">{{ sub.venue }}</span>{% endif %}
                <p class="card-text">{{ sub.description }}</p>
                <div class="oss-links">
                  {% for link in sub.links %}
                    <a class="btn btn-sm" href="{{ link.url }}" target="_blank" rel="noopener noreferrer"><i class="{{ link.icon }}"></i> {{ link.label }}</a>
                  {% endfor %}
                  {% for paper in sub.papers %}
                    <a class="btn btn-sm" href="https://arxiv.org/abs/{{ paper.arxiv }}" target="_blank" rel="noopener noreferrer"
                      ><i class="ai ai-arxiv"></i> {{ paper.label }}</a
                    >
                  {% endfor %}
                </div>
              </div>
            {% endfor %}
          </div>
        {% endif %}
      </div>
    </div>
  {% endfor %}
</div>
