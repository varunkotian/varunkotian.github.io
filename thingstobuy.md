---
layout: page
title: Things To Buy
permalink: /thingstobuy/
---

<style>
  :root {
    --tb-bg: #f7f5f0;
    --tb-card: #fffdfa;
    --tb-ink: #1f2933;
    --tb-muted: #6b7280;
    --tb-accent: #0f766e;
    --tb-border: #e9e2d8;
    --tb-pri-1: #b91c1c;
    --tb-pri-2: #b45309;
    --tb-pri-3: #166534;
  }

  body, .page-content, .wrapper {
    background: radial-gradient(circle at 20% 20%, #fffdf7 0%, var(--tb-bg) 55%, #efe8dc 100%) !important;
    color: var(--tb-ink) !important;
  }

  .tb-header {
    margin: 0.4rem 0 1.1rem;
  }

  .tb-title {
    margin: 0;
    font-size: 1.95rem;
    letter-spacing: 0.02em;
  }

  .tb-subtitle {
    margin: 0.45rem 0 0;
    color: var(--tb-muted);
  }

  .tb-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(255px, 1fr));
    gap: 0.9rem;
    margin: 0.9rem 0 1.6rem;
  }

  .tb-card {
    border: 1px solid var(--tb-border);
    background: var(--tb-card);
    border-radius: 12px;
    padding: 0.85rem 0.9rem;
    box-shadow: 0 1px 10px rgba(15, 23, 42, 0.05);
  }

  .tb-item-title {
    font-weight: 700;
    margin-bottom: 0.25rem;
  }

  .tb-meta {
    color: var(--tb-muted);
    font-size: 0.92rem;
    margin-bottom: 0.45rem;
  }

  .tb-priority {
    display: inline-block;
    padding: 0.15rem 0.5rem;
    border-radius: 999px;
    font-size: 0.8rem;
    font-weight: 700;
    margin-right: 0.45rem;
    color: #fff;
  }

  .tb-p1 { background: var(--tb-pri-1); }
  .tb-p2 { background: var(--tb-pri-2); }
  .tb-p3 { background: var(--tb-pri-3); }

  .tb-section {
    margin-top: 1.25rem;
  }

  .tb-section h2 {
    margin-bottom: 0.5rem;
  }

  .tb-empty {
    color: var(--tb-muted);
    font-style: italic;
  }

  .tb-replace {
    margin-top: 0.35rem;
    font-size: 0.9rem;
  }

  @media (max-width: 560px) {
    .tb-title { font-size: 1.55rem; }
  }
</style>

{% assign all_items = site.data.thingstobuy %}
{% assign need_items = all_items | where: "status", "Need" | sort: "priority_order" %}
{% assign planned_items = all_items | where: "status", "Planned" | sort: "priority_order" %}
{% assign ordered_items = all_items | where: "status", "Ordered" %}
{% assign bought_items = all_items | where: "status", "Bought" %}

<div class="tb-header">
  <h1 class="tb-title">Things To Buy</h1>
  <p class="tb-subtitle">Long-term buy list with replacement cadence. Need and Planned are sorted by priority.</p>
</div>

<div class="tb-section">
  <h2>Need (priority-sorted)</h2>
  {% if need_items.size > 0 %}
  <div class="tb-grid">
    {% for item in need_items %}
    <article class="tb-card">
      <div class="tb-item-title">{{ item.name }}</div>
      <div class="tb-meta">{{ item.category }} | Target: {{ item.target_date }} | EUR {{ item.expected_cost_eur }}</div>
      {% if item.priority_order == 1 %}
      <span class="tb-priority tb-p1">{{ item.priority_label | default: "P1" }}</span>
      {% elsif item.priority_order == 2 %}
      <span class="tb-priority tb-p2">{{ item.priority_label | default: "P2" }}</span>
      {% else %}
      <span class="tb-priority tb-p3">{{ item.priority_label | default: "P3" }}</span>
      {% endif %}
      {% if item.replacement_cadence and item.replacement_cadence != "" %}
      <div class="tb-replace">Replacement: {{ item.replacement_cadence }}</div>
      {% endif %}
      {% if item.notes and item.notes != "" %}
      <div class="tb-replace">Note: {{ item.notes }}</div>
      {% endif %}
    </article>
    {% endfor %}
  </div>
  {% else %}
  <p class="tb-empty">No items in Need.</p>
  {% endif %}
</div>

<div class="tb-section">
  <h2>Planned (priority-sorted)</h2>
  {% if planned_items.size > 0 %}
  <div class="tb-grid">
    {% for item in planned_items %}
    <article class="tb-card">
      <div class="tb-item-title">{{ item.name }}</div>
      <div class="tb-meta">{{ item.category }} | Target: {{ item.target_date }} | EUR {{ item.expected_cost_eur }}</div>
      {% if item.priority_order == 1 %}
      <span class="tb-priority tb-p1">{{ item.priority_label | default: "P1" }}</span>
      {% elsif item.priority_order == 2 %}
      <span class="tb-priority tb-p2">{{ item.priority_label | default: "P2" }}</span>
      {% else %}
      <span class="tb-priority tb-p3">{{ item.priority_label | default: "P3" }}</span>
      {% endif %}
      {% if item.replacement_cadence and item.replacement_cadence != "" %}
      <div class="tb-replace">Replacement: {{ item.replacement_cadence }}</div>
      {% endif %}
      {% if item.notes and item.notes != "" %}
      <div class="tb-replace">Note: {{ item.notes }}</div>
      {% endif %}
    </article>
    {% endfor %}
  </div>
  {% else %}
  <p class="tb-empty">No items in Planned.</p>
  {% endif %}
</div>

<div class="tb-section">
  <h2>Ordered</h2>
  {% if ordered_items.size > 0 %}
  <div class="tb-grid">
    {% for item in ordered_items %}
    <article class="tb-card">
      <div class="tb-item-title">{{ item.name }}</div>
      <div class="tb-meta">{{ item.category }} | Target: {{ item.target_date }} | EUR {{ item.expected_cost_eur }}</div>
      {% if item.notes and item.notes != "" %}
      <div class="tb-replace">Note: {{ item.notes }}</div>
      {% endif %}
    </article>
    {% endfor %}
  </div>
  {% else %}
  <p class="tb-empty">No items in Ordered.</p>
  {% endif %}
</div>

<div class="tb-section">
  <h2>Bought</h2>
  {% if bought_items.size > 0 %}
  <div class="tb-grid">
    {% for item in bought_items %}
    <article class="tb-card">
      <div class="tb-item-title">{{ item.name }}</div>
      <div class="tb-meta">{{ item.category }} | Target: {{ item.target_date }} | EUR {{ item.expected_cost_eur }}</div>
      {% if item.notes and item.notes != "" %}
      <div class="tb-replace">Note: {{ item.notes }}</div>
      {% endif %}
    </article>
    {% endfor %}
  </div>
  {% else %}
  <p class="tb-empty">No items in Bought.</p>
  {% endif %}
</div>
