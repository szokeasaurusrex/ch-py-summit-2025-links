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

<div class="meta">{{ page.subtitle }}</div>
{% endif %}

<div class="meta">
  {{ page.event }} · <span>{{ page.date }}</span> · <span>{{ page.location }}</span>
  </div>
<div class="meta">Speaker: <strong>{{ page.speaker_name }}</strong></div>

## Quick links

<div id="links" class="links" markdown="1">
{% for link in site.data.links %}
- [{{ link.title }}]({{ link.url }}){% if link.description %}<br /><span class="desc">{{ link.description }}</span>{% endif %}
{% endfor %}
</div>

## About the talk

TBD short abstract (2–4 sentences).

## About the speaker

Hello 👋 My name is Daniel Szoke, and I am a software engineer at [Sentry](https://sentry.io/welcome), where I maintain the [Sentry CLI](https://github.com/getsentry/sentry-cli) and the [Python SDK](https://github.com/getsentry/sentry-python).
