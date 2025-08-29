---
title: "Why you should learn Rust"
subtitle: "As a Python developer"
event: "PyCon GR"
date: "2025-08-30"
location: "Athens 🇬🇷"
speaker_name: "Daniel Szoke"
headshot_src: assets/images/headshot.jpg
description: "Links and resources for TBD talk at PyCon GR."
layout: default
# url: "https://YOUR_USERNAME.github.io"
# baseurl: "/presentation-links"
---

# {{ page.title }}

{% if page.subtitle %}

<p class="subtitle">{{ page.subtitle }}</p>
{% endif %}

## Talk info

<div class="event-meta">
  <span class="event">{{ page.event }}</span> · 
  <span class="date">{{ page.date }}</span> · 
  <span class="location">{{ page.location }}</span>
</div>
<div class="speaker-meta">Speaker: <strong>{{ page.speaker_name }}</strong></div>

## Quick links

<div class="card-grid">
{% for link in site.data.links %}
<a href="{{ link.url }}" class="link-card">
  <header>
    <h3 markdown="1">{{ link.title }}</h3>
  </header>
  {% if link.description %}
  <p class="card-description" markdown="1">{{ link.description }}</p>
  {% endif %}
</a>
{% endfor %}
</div>

## About me

Hello 👋 My name is Daniel Szoke, and I am a software engineer at [Sentry](https://sentry.io/welcome), where I maintain the [Sentry CLI](https://github.com/getsentry/sentry-cli) and the [Python SDK](https://github.com/getsentry/sentry-python).
