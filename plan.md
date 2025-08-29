## Plan: Markdown Site for PyCon GR Presentation Links (GitHub Pages)

### Goals and Constraints

- **Purpose**: A single-page static site with a curated list of links relevant to a PyCon GR talk.
- **Design**: Beautiful yet minimalist; clear hierarchy; high contrast and generous spacing.
- **Mobile-first**: Optimized for phones (QR traffic), scales gracefully to desktop.
- **Easy to extend**: Adding links should be trivial without touching layout.
- **Content**: Links, short talk info, short speaker bio; optional sponsor note (Sentry).
- **Hosting**: GitHub Pages (project site).
- **Authoring format**: Markdown-first, rendered by GitHub Pages (Jekyll + Liquid). No custom build required.

### Recommended Approach (Markdown, powered by GitHub Pages)

- **Stack**: Markdown (`index.md`) + Jekyll data (`_data/links.yml`) + Liquid templating. Optional small CSS override.
- **Data-driven links**: Maintain links in `_data/links.yml` and render via a simple Liquid loop in `index.md` so adding links is one line per link.
- **Progressive enhancement**: If data is missing, the page should still render with a brief note or a minimal fallback.

### Repository Structure

```
.
├── index.md
├── _data/
│   └── links.yml
├── assets/
│   ├── images/           # (optional) headshot, logos
│   └── icons/            # favicons
├── assets/css/
│   └── custom.css        # (optional) small style tweaks
├── _config.yml
├── instructions.md       # human-facing fill-in guide for placeholders
└── README.md
```

### Content Model (placeholders)

- **Talk metadata** (front matter in `index.md`):

```yaml
---
title: "TBD Talk Title"
subtitle: "TBD Subtitle"
event: "PyCon GR"
date: "TBD"
location: "TBD"
speaker_name: "TBD Your Name"
bio_short: "TBD short bio (1–2 sentences)."
sponsor_note: "Trip financed by Sentry."
headshot_src: assets/images/headshot.jpg # optional
description: "Links and resources for TBD talk at PyCon GR."
layout: default
# For project pages:
# baseurl: "/presentation-links"
# url: "https://YOUR_USERNAME.github.io"
---
```

- **Links data** in `_data/links.yml`:

```yaml
- title: "Rust Book"
  url: "https://example.com/rust-book"
  description: "TBD short description."
  category: "Learning"
  icon: "rust"
  pin: true

- title: "My GitHub"
  url: "https://github.com/YOUR_USERNAME"
  description: "TBD."
  category: "Profiles"
  icon: "github"

- title: "My LinkedIn"
  url: "https://www.linkedin.com/in/YOUR_HANDLE"
  description: "TBD."
  category: "Profiles"
  icon: "linkedin"

- title: "Sentry"
  url: "https://sentry.io/"
  description: "Company financing the trip."
  category: "Sponsor"
  icon: "sentry"
  highlight: true

- title: "Slides"
  url: "https://example.com/slides.pdf"
  description: "Slide deck (PDF/URL)."
  category: "Talk"
  icon: "slides"
  pin: true
```

### Design System

- **Typography**: System fonts for performance. Fluid type via CSS clamp if customizing.
- **Colors**: Use a lightweight CSS override with variables and auto dark mode via `prefers-color-scheme` if desired.
- **Layout**: Narrow content width, ample whitespace, touch-friendly targets.
- **Link cards**: Presented as a clean list in Markdown; optionally styled via `assets/css/custom.css`.
- **Icons**: Optional small inline SVGs or emoji for recognition.

Optional CSS variables starter (put in `assets/css/custom.css` and include via `_config.yml`):

```css
:root {
  --bg: #ffffff;
  --fg: #111111;
  --muted: #666666;
  --card: #f7f7f8;
  --accent: #4f46e5; /* indigo */
  --radius: 14px;
  --shadow: 0 1px 2px rgba(0, 0, 0, 0.06), 0 6px 20px rgba(0, 0, 0, 0.08);
}
@media (prefers-color-scheme: dark) {
  :root {
    --bg: #0b0c0f;
    --fg: #f3f4f6;
    --muted: #9ca3af;
    --card: #151821;
    --accent: #8b5cf6; /* violet */
    --shadow: 0 1px 2px rgba(0, 0, 0, 0.5), 0 10px 30px rgba(0, 0, 0, 0.6);
  }
}
body {
  margin: 0;
  background: var(--bg);
  color: var(--fg);
  font-family: ui-sans-serif, -apple-system, Segoe UI, Roboto, Ubuntu,
    Cantarell, Noto Sans, Helvetica Neue, Arial, "Apple Color Emoji",
    "Segoe UI Emoji";
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
.badge {
  color: var(--accent);
  font-weight: 600;
  font-size: 0.85rem;
}
.desc {
  color: var(--muted);
}
```

To load `custom.css`, add to `_config.yml` (see `_config.yml` section below).

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
sponsor_note: "Trip financed by Sentry."
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
{% assign pinned = site.data.links | where_exp: "l", "l.pin" %}
{% assign others = site.data.links | where_exp: "l", "l.pin != true" %}
{% assign sorted = pinned | concat: others %}
{% for link in sorted %}
- [{{ link.title }}]({{ link.url }}){% if link.highlight %} <span class="badge">Sponsor</span>{% endif %}{% if link.description %}<br /><span class="desc">{{ link.description }}</span>{% endif %}
{% endfor %}
</div>

## About the talk

TBD short abstract (2–4 sentences).

## About the speaker

{{ page.bio_short }}{% if page.sponsor_note %} {{ page.sponsor_note }}{% endif %}

<footer class="meta">© {{ "now" | date: "%Y" }} {{ page.speaker_name }}</footer>
```

### `_config.yml` (GitHub Pages settings)

- Set a theme and add `custom.css` if used. For project pages, also set `url` and `baseurl`.

```yaml
title: "PyCon GR Presentation Links"
description: "Links and resources for the talk."
theme: minima # or a Pages theme (e.g., jekyll-theme-cayman)
# For project pages:
# url: "https://YOUR_USERNAME.github.io"
# baseurl: "/presentation-links"

# Include custom CSS (for minima):
plugins:
  - jekyll-include-cache
# Add the following to include assets/css/custom.css:
# In minima, create _includes/head-custom.html with a <link> tag,
# or use a theme that supports additional stylesheets directly.
```

Minimal `head` include (optional, if you want to load `custom.css` with minima):

```
_includes/head-custom.html
<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">
```

And ensure `_layouts/default.html` (from theme) includes `head-custom.html` if supported; otherwise switch to a theme that supports custom head includes or copy a minimal default layout.

### Accessibility Checklist

- Proper headings and section structure in Markdown.
- Sufficient color contrast in both light/dark.
- Keyboard focus visible (theme dependent).
- Touch targets ≥ 44×44 px; spacing between list items/cards.
- Link text descriptive (not just "click here").

### Performance and SEO

- Small, static footprint; no custom JS by default.
- Use front matter `description` and proper title.
- Provide favicons and a high-res social image (optional).
- Consider `social` image metadata via theme or custom head include.

### Local Development

- No build is required if relying on GitHub Pages to render. Commit and push to preview live.
- Optional: Preview locally with Jekyll if desired:
  - Install Ruby and Bundler, then run:
    ```bash
    bundle init && bundle add jekyll && bundle exec jekyll new --skip-bundle .
    bundle exec jekyll serve
    ```
  - Visit `http://localhost:4000`.

### GitHub Pages Deployment

- Use a project page: `https://YOUR_USERNAME.github.io/presentation-links/`.
- In GitHub repo Settings → Pages:
  - **Source**: Deploy from a branch
  - **Branch**: `main` (root)
- If using project pages, set `url` and `baseurl` in `_config.yml` as shown.
- Commit and push; Pages will auto-build in ~1–2 minutes.
- Optional: Custom domain via `CNAME` file at repo root.

### How to Add or Update Links (future maintenance)

- Edit `_data/links.yml` and append a new item with `title`, `url`, optional `description`, `category`, `icon`, `pin`, `highlight`.
- No need to change Markdown unless you want new sections or different layout.

### Instructions File (`instructions.md`)

Create `instructions.md` at the repo root. It should guide a human to fill in all placeholders and publish:

- **Update talk metadata**: Open `index.md` and replace all `TBD` values in front matter (`title`, `subtitle`, `event`, `date`, `location`, `speaker_name`, `bio_short`, `sponsor_note`, `headshot_src`, `description`).
- **Add links**: Open `_data/links.yml` and:
  - Duplicate an existing item, update `title`, `url`, and `description`.
  - Optionally set `pin: true` to show at the top.
  - Optionally set `highlight: true` for sponsor/featured links.
- **Assets**: Place images in `assets/images/` and update `headshot_src` or any image references accordingly.
- **Favicons**: Add icons to `assets/icons/` and, if needed, choose a theme or custom head include that references them.
- **Theme and styling**:
  - If using a custom CSS file, edit `assets/css/custom.css` for colors, spacing, and typography.
  - Ensure it’s loaded via theme support (see `_config.yml` notes).
- **URLs for project page**:
  - In `_config.yml`, set `url` to `https://YOUR_USERNAME.github.io` and `baseurl` to `/presentation-links`.
- **Publish**:
  - Commit changes and push to `main`.
  - Verify at `https://YOUR_USERNAME.github.io/presentation-links/`.
- **Troubleshooting**:
  - If the page doesn’t update, check the Pages build logs in GitHub → Actions or Settings → Pages.
  - Validate YAML formatting in `_data/links.yml` (consistent indentation, hyphens for list items).

### Acceptance Criteria

- Page loads fast and looks excellent on small screens.
- At least the five placeholder links are present and tappable:
  - Rust Book, GitHub, LinkedIn, Sentry (highlighted), Slides (pinned)
- Includes sections: Quick links, About the talk, About the speaker.
- Dark mode adapts automatically if the chosen theme supports it or via `custom.css`.
- Works without console errors; Lighthouse scores (when tested on rendered HTML): A11y ≥ 95, SEO ≥ 90.

### Optional Enhancements (nice-to-have)

- Add icons (small inline SVG or emoji) beside each link type.
- Add copy-to-clipboard button for the slides URL (progressive enhancement).
- Generate a QR code image linking to the site for slide embedding.
- Basic analytics (privacy-friendly), e.g., Plausible/Umami (via custom head include).
- Service Worker for offline cache (if adopting a more advanced setup).

### Next Actions (for the agent)

1. Scaffold directories and files as above (Markdown + Jekyll).
2. Create `_config.yml` with a theme and optional CSS include.
3. Paste the `index.md` skeleton and commit.
4. Populate `_data/links.yml` with the placeholders provided here.
5. Add `instructions.md` with the steps outlined above.
6. Enable GitHub Pages and verify the live URL.
