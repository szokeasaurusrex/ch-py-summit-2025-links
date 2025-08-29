## Plan: Markdown Site for PyCon GR Presentation Links (GitHub Pages)

### Goals and Constraints

- **Purpose**: A simple, fast single-page site with links relevant to a PyCon GR talk.
- **Design**: Minimalist, readable, high contrast, works great on phones.
- **Authoring**: Markdown-first, rendered by GitHub Pages (Jekyll + Liquid). No custom build.
- **Hosting**: GitHub Pages (project site).

### Approach (Markdown + Jekyll)

- **Stack**: `index.md` + Jekyll data file `_data/links.yml` + minimal Liquid loop.
- **Data**: Keep links as a plain list with `title`, `url`, and optional `description`.
- **Styling**: Use theme defaults; optional small CSS (`assets/css/custom.css`).

### Repository Structure

```
.
├── index.md
├── _data/
│   └── links.yml
├── assets/
│   ├── images/           # optional (headshot, social image)
│   └── css/
│       └── custom.css    # optional
├── _config.yml
├── instructions.md       # how to fill placeholders and publish
└── README.md
```

### Content Model

- **Talk metadata** (front matter in `index.md`):

```yaml
---
title: "TBD Talk Title"
subtitle: "TBD Subtitle"
event: "PyCon GR"
date: "TBD"
location: "TBD"
speaker_name: "TBD Your Name"
bio_short: "TBD short bio (1–2 sentences)." # e.g., "Software engineer at Sentry."
headshot_src: assets/images/headshot.jpg # optional
description: "Links and resources for TBD talk at PyCon GR."
layout: default
# For project pages:
# baseurl: "/presentation-links"
# url: "https://YOUR_USERNAME.github.io"
---
```

- **Links data** in `_data/links.yml` (order is manual; no pinning/highlights):

```yaml
- title: "Slides"
  url: "https://example.com/slides.pdf"
  description: "Slide deck (PDF/URL)."

- title: "Rust Book"
  url: "https://example.com/rust-book"
  description: "Comprehensive guide to Rust."

- title: "My GitHub"
  url: "https://github.com/YOUR_USERNAME"
  description: "Code and projects."

- title: "My LinkedIn"
  url: "https://www.linkedin.com/in/YOUR_HANDLE"
  description: "Background and contact."
```

### Optional CSS (tiny override)

If desired, add a small stylesheet at `assets/css/custom.css` and include it via the theme (see `_config.yml`).

```css
body {
  line-height: 1.6;
}
.container {
  max-width: 44rem;
  margin: 0 auto;
  padding: 1.25rem;
}
.links {
  display: grid;
  gap: 0.75rem;
}
.desc {
  color: #666;
}
```

### Markdown Skeleton (`index.md`)

```markdown
---
title: "TBD Talk Title"
subtitle: "TBD Subtitle"
event: "PyCon GR"
date: "TBD"
location: "TBD"
speaker_name: "TBD Your Name"
bio_short: "TBD short bio (1–2 sentences)."
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

<div id="links" class="links">
{% for link in site.data.links %}
- [{{ link.title }}]({{ link.url }}){% if link.description %}<br /><span class="desc">{{ link.description }}</span>{% endif %}
{% endfor %}
</div>

## About the talk

TBD short abstract (2–4 sentences).

## About the speaker

{{ page.bio_short }}

<footer class="meta">© {{ "now" | date: "%Y" }} {{ page.speaker_name }}</footer>
```

### `_config.yml` (GitHub Pages)

- Use a supported theme (e.g., `minima`). If adding `custom.css`, load it via a head include as supported by the theme.

```yaml
title: "PyCon GR Presentation Links"
description: "Links and resources for the talk."
theme: minima
# For project pages:
# url: "https://YOUR_USERNAME.github.io"
# baseurl: "/presentation-links"

# If your theme supports head includes, add `_includes/head-custom.html` with:
# <link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">
```

### Accessibility, Performance, SEO

- Use proper headings and clear link text.
- Keep contrast high; ensure mobile tap targets are comfortable.
- Keep the page static and lightweight; set a descriptive title and `description`.

### Local Development

- No build required; commit and push to preview on Pages.
- Optional local preview with Jekyll:
  - Install Ruby and Bundler, then:
    ```bash
    bundle init && bundle add jekyll && bundle exec jekyll new --skip-bundle .
    bundle exec jekyll serve
    ```
  - Visit `http://localhost:4000`.

### GitHub Pages Deployment

- Project page URL: `https://YOUR_USERNAME.github.io/presentation-links/`.
- In repo Settings → Pages: Source = Deploy from a branch; Branch = `main` (root).
- If using a project page, set `url` and `baseurl` in `_config.yml`.

### Maintenance: Adding/Updating Links

- Edit `_data/links.yml` and add items with `title`, `url`, and optional `description`.
- Order the list manually as desired.

### Instructions (`instructions.md`)

Guide a human to:

- Replace `TBD` values in `index.md` front matter (title, subtitle, event, date, location, speaker_name, bio_short, headshot_src, description). If relevant, you can mention your employer in `bio_short` (e.g., "I work at Sentry.").
- Add links in `_data/links.yml` (title, url, optional description).
- Optional: Add images to `assets/images/` and include as needed.
- Optional: Add `assets/css/custom.css` and ensure it is loaded by the theme.
- For project pages, set `url` and `baseurl` in `_config.yml`.
- Commit, push, and verify on GitHub Pages.

### Acceptance Criteria

- Page renders correctly on mobile and desktop.
- Contains at least these links: Slides, Rust Book, GitHub, LinkedIn.
- Includes sections: Quick links, About the talk, About the speaker.
- No sponsor badges, pinning, or special link states.

### Next Actions

1. Scaffold files and directories.
2. Create `_config.yml` with a theme (minima or equivalent).
3. Add `index.md` skeleton and commit.
4. Populate `_data/links.yml` with placeholders.
5. Add `instructions.md` with the steps above.
6. Enable GitHub Pages and verify the live URL.
