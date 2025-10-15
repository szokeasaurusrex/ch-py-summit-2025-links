---
title: "Why you should learn Rust 🦀"
subtitle: "As a Python developer 🐍"
event: "Swiss Python Summit"
date: "2025-10-16"
location: "Ostschweizer Fachhochschule, Rapperswil 🇨🇭"
speaker_name: "Daniel Szoke"
headshot_src: assets/images/headshot.jpg
description: "Links and resources for my talk at Swiss Python Summit."
layout: default
url: "https://szokeasaurusrex.github.io"
baseurl: "/ch-py-summit-2025-links"
---

# {{ page.title }}

{% if page.subtitle %}

<div class="subtitle">{{ page.subtitle }}</div>
{% endif %}

_by {{ page.speaker_name }}_

<br />

🎤 {{ page.event }}
<br />
📅 {{ page.date }}
<br />
📍 {{ page.location }}

## Join our team! 💼

**Sentry is hiring!**

🐍 _Python expert?_ My Vienna-based team is seeking a [**Senior Software Engineer** to work on Sentry's **Python SDK**](https://jobs.ashbyhq.com/sentry/d8b87888-f749-40c4-a115-c82f1b5cb5f7?utm_source=WOZEA5nmQN).

👩‍🎓 _Ambitious student?_ Check out our [**New Grad**](https://jobs.ashbyhq.com/sentry/aedee875-ffca-477a-bc8c-1347628cc596?utm_source=wqvaGJA871) and [**Intern**](https://jobs.ashbyhq.com/sentry/a37972b3-e3e1-4a47-9302-a216d54e3d37?utm_source=z6NZ1a5Rgk) positions!

✨ _Something else?_ We have [**more than forty open positions**](https://jobs.ashbyhq.com/sentry?utm_source=WoEaZQXbgY) across all locations, including [**five in Vienna**](https://jobs.ashbyhq.com/sentry?locationId=63ea26ea-e529-472a-93cc-fbd1a85c9941&utm_source=WoEaZQXbgY), our European hub.

**Please apply using the links above**, so we know you heard about us from the Swiss Python Summit 🏔️🐍

## Quick links 🔗

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

## About me 🙋🏼

Hello 👋 My name is Daniel Szoke, and I am a software engineer at [Sentry](https://sentry.io/welcome), where I maintain the [Sentry CLI](https://github.com/getsentry/sentry-cli) and occasionally the [Python SDK](https://github.com/getsentry/sentry-python).
