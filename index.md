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

## Sentry is hiring! 💼

<div class="card-grid">
  <div class="job-card">
    <header>
      <h3>🐍 Python expert?</h3>
    </header>
    <p class="card-description">
      My Vienna-based team is seeking a <a href="https://jobs.ashbyhq.com/sentry/d8b87888-f749-40c4-a115-c82f1b5cb5f7?utm_source=WOZEA5nmQN"><strong>Senior Software Engineer</strong></a> to work on Sentry's <strong>Python SDK</strong>.
    </p>
  </div>

  <div class="job-card">
    <header>
      <h3>👩‍🎓 Ambitious student?</h3>
    </header>
    <p class="card-description">
      Check out our <a href="https://jobs.ashbyhq.com/sentry/aedee875-ffca-477a-bc8c-1347628cc596?utm_source=wqvaGJA871"><strong>New Grad</strong></a> and <a href="https://jobs.ashbyhq.com/sentry/a37972b3-e3e1-4a47-9302-a216d54e3d37?utm_source=z6NZ1a5Rgk"><strong>Intern</strong></a> positions!
    </p>
  </div>

  <div class="job-card">
    <header>
      <h3>✨ Something else?</h3>
    </header>
    <p class="card-description">
      We have <a href="https://jobs.ashbyhq.com/sentry?utm_source=WoEaZQXbgY"><strong>more than forty open positions</strong></a> across all locations, including <a href="https://jobs.ashbyhq.com/sentry?locationId=63ea26ea-e529-472a-93cc-fbd1a85c9941&utm_source=WoEaZQXbgY"><strong>five in Vienna</strong></a>, our European hub.
    </p>
  </div>
</div>

**Please apply using the links above**, so we know you heard about us from the Swiss Python Summit 🏔️🐍

## Resources & other links 🔗

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
