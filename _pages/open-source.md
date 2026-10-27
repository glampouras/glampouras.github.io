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
  /* link tints by destination; redefined for dark mode below */
  :root {
    --oss-github: #24292f;
    --oss-hf: #a86500;
    --oss-paper: #b31b1b;
    --oss-shadow: rgba(0, 0, 0, 0.12);
  }
  html[data-theme="dark"] {
    --oss-github: #e6edf3;
    --oss-hf: #ffcc4d;
    --oss-paper: #ff7b72;
    --oss-shadow: rgba(0, 0, 0, 0.45);
  }

  .oss-list {
    display: flex;
    flex-direction: column;
    gap: 1.25rem;
  }

  /* cards: accent stripe + hover lift */
  .oss-card {
    border-left: 4px solid var(--global-theme-color);
    transition:
      transform 0.15s ease,
      box-shadow 0.15s ease;
  }
  .oss-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 18px var(--oss-shadow);
  }
  .oss-card .card-title {
    color: var(--global-theme-color);
    margin-bottom: 0.25rem;
  }

  /* featured card: tinted background, heavier stripe, larger title */
  .oss-featured {
    border-left-width: 6px;
    background: color-mix(in srgb, var(--global-theme-color) 7%, var(--global-card-bg-color));
  }
  .oss-featured .card-title {
    font-size: 1.75rem;
  }
  .oss-eyebrow {
    font-size: 0.75rem;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--global-theme-color);
    margin-bottom: 0.25rem;
  }

  /* topic chips */
  .oss-tags {
    margin: 0.4rem 0 0.6rem;
  }
  .oss-tag {
    display: inline-block;
    font-size: 0.78rem;
    padding: 0.1rem 0.6rem;
    margin: 0 0.3rem 0.3rem 0;
    border-radius: 999px;
    color: var(--global-theme-color);
    background: color-mix(in srgb, var(--global-theme-color) 12%, transparent);
  }

  /* subcards */
  .oss-subgrid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 1rem;
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

  /* link buttons, tinted by destination */
  .oss-links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-top: 0.75rem;
  }
  .oss-links .btn {
    --oss-link: var(--global-theme-color);
    margin: 0;
    font-size: 0.95rem;
    padding: 0.3rem 0.75rem;
    border-radius: 0.375rem;
    color: var(--oss-link);
    border: 1px solid var(--oss-link);
  }
  .oss-links .btn[href*="github.com"] {
    --oss-link: var(--oss-github);
  }
  .oss-links .btn[href*="huggingface.co"] {
    --oss-link: var(--oss-hf);
  }
  .oss-links .btn[href*="arxiv.org"] {
    --oss-link: var(--oss-paper);
  }
  .oss-links .btn:hover {
    color: var(--global-card-bg-color);
    background: var(--oss-link);
    border-color: var(--oss-link);
  }
  .oss-links-cols {
    display: grid;
    grid-template-columns: repeat(var(--oss-cols), minmax(0, 1fr));
  }
  .oss-links-cols .btn {
    text-align: center;
    white-space: normal;
  }
  @media (max-width: 576px) {
    .oss-links-cols {
      grid-template-columns: 1fr;
    }
  }
</style>

<div class="oss-list">
  {% for project in site.data.open_source %}
    <div class="card oss-card{% if project.featured %} oss-featured{% endif %}">
      <div class="card-body">
        {% if project.featured %}<div class="oss-eyebrow">{{ project.featured }}</div>{% endif %}
        <h3 class="card-title">{{ project.title }}</h3>
        {% if project.venue %}<span class="badge">{{ project.venue }}</span>{% endif %}
        {% if project.tags %}
          <div class="oss-tags">
            {% for tag in project.tags %}<span class="oss-tag">{{ tag }}</span>{% endfor %}
          </div>
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
          <div class="oss-subgrid">
            {% for sub in project.subprojects %}
              <div class="oss-sub">
                <h4>{{ sub.title }}</h4>
                {% if sub.venue %}<span class="badge">{{ sub.venue }}</span>{% endif %}
                {% if sub.tags %}
                  <div class="oss-tags">
                    {% for tag in sub.tags %}<span class="oss-tag">{{ tag }}</span>{% endfor %}
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
