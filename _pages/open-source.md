---
layout: page
permalink: /open-source/
title: open source code
description: Code, datasets, and benchmarks released alongside our research.
nav: true
nav_order: 2
---

<!-- Content lives in _data/open_source.yml; styles in _sass/_custom.scss -->

<div class="oss-list">
  {% for project in site.data.open_source %}
    <div class="card gl-card{% if project.featured %} oss-featured{% endif %}">
      <div class="card-body">
        <div class="oss-head">
          {% if project.logo %}
            <img class="oss-logo" src="{{ project.logo | prepend: '/assets/logos/' | relative_url }}" alt="{{ project.title }} logo" loading="lazy">
          {% endif %}
          <div class="oss-head-text">
            {% if project.featured %}<div class="oss-eyebrow">{{ project.featured }}</div>{% endif %}
            <h3 class="card-title">{{ project.title }}</h3>
            {% if project.venue %}<span class="badge">{{ project.venue }}</span>{% endif %}
            {% if project.tags %}
              <div class="gl-chips">
                {% for tag in project.tags %}<span class="gl-chip">{{ tag }}</span>{% endfor %}
              </div>
            {% endif %}
          </div>
        </div>
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
          <div class="oss-subgrid">
            {% for sub in project.subprojects %}
              <div class="oss-sub">
                <h4>{{ sub.title }}</h4>
                {% if sub.venue %}<span class="badge">{{ sub.venue }}</span>{% endif %}
                {% if sub.tags %}
                  <div class="gl-chips">
                    {% for tag in sub.tags %}<span class="gl-chip">{{ tag }}</span>{% endfor %}
                  </div>
                {% endif %}
                {% if sub.description %}<p class="card-text">{{ sub.description }}</p>{% endif %}
                <div class="oss-links{% if sub.columns %} oss-links-cols{% endif %}"{% if sub.columns %} style="--oss-cols: {{ sub.columns }}"{% endif %}>
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
