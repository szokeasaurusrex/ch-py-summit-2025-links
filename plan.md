## Plan: Static Site for PyCon GR Presentation Links (GitHub Pages)

### Goals and Constraints

- **Purpose**: A single-page static site with a curated list of links relevant to a PyCon GR talk.
- **Design**: Beautiful yet minimalist; clear hierarchy; high contrast and generous spacing.
- **Mobile-first**: Optimized for phones (QR traffic), scales gracefully to desktop.
- **Easy to extend**: Adding links should be trivial without touching layout.
- **Content**: Links, short talk info, short speaker bio; optional sponsor note (Sentry).
- **Hosting**: GitHub Pages (project site).

### Recommended Approach (no build tools)

- **Stack**: Vanilla HTML + CSS + minimal JS. No frameworks. No bundler.
- **Data-driven links**: Maintain links in `data/links.json` and render via a tiny `scripts/app.js` so adding new links is one-line-per-link.
- **Progressive enhancement**: Provide a graceful fallback (links hard-coded in HTML if JS is disabled) if desired.

### Repository Structure

```
.
├── index.html
├── styles/
│   └── main.css
├── scripts/
│   └── app.js
├── data/
│   └── links.json
├── assets/
│   ├── images/           # (optional) headshot, logos
│   └── icons/            # favicons
├── CNAME                 # optional custom domain
└── README.md
```

### Content Model (placeholders)

- **Talk metadata** (in `index.html` or `data/talk.json` if preferred):

  - `talk_title`: "TBD Talk Title"
  - `talk_subtitle`: "TBD Subtitle"
  - `event`: "PyCon GR"
  - `date`: "TBD"
  - `location`: "TBD"
  - `speaker_name`: "TBD Your Name"
  - `bio_short`: "TBD short bio (1–2 sentences)."
  - `sponsor_note`: "Trip financed by Sentry."
  - `headshot_src`: `assets/images/headshot.jpg` (optional)

- **Links data** in `data/links.json`:

```json
[
  {
    "title": "Rust Book",
    "url": "https://example.com/rust-book",
    "description": "TBD short description.",
    "category": "Learning",
    "icon": "rust",
    "pin": true
  },
  {
    "title": "My GitHub",
    "url": "https://github.com/YOUR_USERNAME",
    "description": "TBD.",
    "category": "Profiles",
    "icon": "github"
  },
  {
    "title": "My LinkedIn",
    "url": "https://www.linkedin.com/in/YOUR_HANDLE",
    "description": "TBD.",
    "category": "Profiles",
    "icon": "linkedin"
  },
  {
    "title": "Sentry",
    "url": "https://sentry.io/",
    "description": "Company financing the trip.",
    "category": "Sponsor",
    "icon": "sentry",
    "highlight": true
  },
  {
    "title": "Slides",
    "url": "https://example.com/slides.pdf",
    "description": "Slide deck (PDF/URL).",
    "category": "Talk",
    "icon": "slides",
    "pin": true
  }
]
```

### Design System

- **Typography**: System fonts for performance. Fluid type using clamp().
- **Colors**: CSS variables and auto dark mode via `prefers-color-scheme`.
- **Layout**: Narrow content width, ample whitespace, touch-friendly targets.
- **Link cards**: Prominent, tappable blocks with subtle elevation/hover.
- **Icons**: Optional small SVGs for quick recognition.

CSS variables starter:

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
html {
  font-size: 16px;
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
h1 {
  font-size: clamp(1.6rem, 4vw, 2.25rem);
  margin: 0 0 0.25rem;
}
h2 {
  font-size: clamp(1.2rem, 3.2vw, 1.5rem);
  margin: 2rem 0 0.75rem;
}
.links {
  display: grid;
  gap: 0.75rem;
}
.card {
  background: var(--card);
  border-radius: var(--radius);
  box-shadow: var(--shadow);
  padding: 0.9rem 1rem;
  transition: transform 0.08s ease, box-shadow 0.2s ease;
}
.card:where(a) {
  color: inherit;
  text-decoration: none;
  display: block;
}
.card:hover {
  transform: translateY(-2px);
}
.card .title {
  font-weight: 600;
}
.card .desc {
  color: var(--muted);
  font-size: 0.95rem;
}
.meta {
  color: var(--muted);
  font-size: 0.95rem;
}
.badge {
  color: var(--accent);
  font-weight: 600;
  font-size: 0.8rem;
}
```

### HTML Skeleton (index.html)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>TBD Talk Title · PyCon GR</title>
    <meta
      name="description"
      content="Links and resources for TBD talk at PyCon GR."
    />
    <meta property="og:title" content="TBD Talk Title · PyCon GR" />
    <meta
      property="og:description"
      content="Links and resources for TBD talk at PyCon GR."
    />
    <meta property="og:type" content="website" />
    <meta
      property="og:url"
      content="https://YOUR_USERNAME.github.io/presentation-links/"
    />
    <link rel="icon" href="assets/icons/favicon.ico" />
    <link rel="stylesheet" href="styles/main.css" />
  </head>
  <body>
    <main class="container">
      <header>
        <h1>TBD Talk Title</h1>
        <div class="meta">
          PyCon GR · <span>TBD Date</span> · <span>TBD Location</span>
        </div>
        <div class="meta">Speaker: <strong>TBD Your Name</strong></div>
      </header>

      <section aria-labelledby="quick-links">
        <h2 id="quick-links">Quick links</h2>
        <div id="links" class="links">
          <!-- JS will render cards from data/links.json -->
          <!-- Optional no-JS fallback: a few static links here -->
        </div>
      </section>

      <section aria-labelledby="about-talk">
        <h2 id="about-talk">About the talk</h2>
        <p class="desc">TBD short abstract (2–4 sentences).</p>
      </section>

      <section aria-labelledby="about-speaker">
        <h2 id="about-speaker">About the speaker</h2>
        <p class="desc">
          TBD short bio. Trip financed by
          <a href="https://sentry.io/" target="_blank" rel="noopener">Sentry</a
          >.
        </p>
      </section>

      <footer class="meta">© <span id="year"></span> TBD Your Name</footer>
    </main>

    <script src="scripts/app.js" defer></script>
    <script>
      document.getElementById("year").textContent = new Date().getFullYear();
    </script>
  </body>
</html>
```

### Minimal Rendering Script (scripts/app.js)

```js
async function fetchLinks() {
  try {
    const response = await fetch("data/links.json", { cache: "no-cache" });
    if (!response.ok) throw new Error("Failed to load links.json");
    return await response.json();
  } catch (error) {
    console.error(error);
    return [];
  }
}

function renderLinkCard(link) {
  const anchor = document.createElement("a");
  anchor.className = "card";
  anchor.href = link.url;
  anchor.target = "_blank";
  anchor.rel = "noopener";

  const title = document.createElement("div");
  title.className = "title";
  title.textContent = link.title;

  const desc = document.createElement("div");
  desc.className = "desc";
  desc.textContent = link.description || "";

  if (link.highlight) {
    const badge = document.createElement("span");
    badge.className = "badge";
    badge.textContent = "Sponsor";
    title.appendChild(document.createTextNode(" "));
    title.appendChild(badge);
  }

  anchor.appendChild(title);
  if (link.description) anchor.appendChild(desc);

  return anchor;
}

(async function init() {
  const container = document.getElementById("links");
  const links = await fetchLinks();

  const pinned = links.filter((l) => l.pin);
  const others = links.filter((l) => !l.pin);
  const sorted = [...pinned, ...others];

  for (const link of sorted) {
    container.appendChild(renderLinkCard(link));
  }
})();
```

### Accessibility Checklist

- Proper landmarks (`<main>`, `<header>`, `<section>`, `<footer>`), `aria-labelledby` for sections.
- Sufficient color contrast in both light/dark.
- Keyboard focus visible and logical.
- Touch targets ≥ 44×44 px; spacing between cards.
- Link text descriptive (not just "click here").

### Performance and SEO

- Small, static footprint; no external CSS/JS by default.
- Add basic meta description and Open Graph/Twitter tags.
- Provide favicons and a high-res social image (optional).
- Consider a print stylesheet for handouts (optional).

### Local Development

1. Create files per structure above.
2. Run a simple local server to test fetch of JSON:

```bash
python3 -m http.server 8080
```

3. Visit `http://localhost:8080` on mobile and desktop; use dev tools to emulate devices.
4. Audit with Lighthouse for Performance/Accessibility/SEO.

### GitHub Pages Deployment

- Use a project page: `https://YOUR_USERNAME.github.io/presentation-links/`.
- In GitHub repo Settings → Pages:
  - Source: **Deploy from a branch**
  - Branch: **main** (root)
- Commit and push; Pages will auto-build in ~1–2 minutes.
- Optional: Custom domain via `CNAME` file at repo root.

### How to Add or Update Links (future maintenance)

- Edit `data/links.json` and append a new object with `title`, `url`, optional `description`, `category`, `icon`, `pin`, `highlight`.
- No need to change HTML/JS unless you want new categories or visual variants.

### Acceptance Criteria

- Page loads fast on 3G and looks excellent on small screens.
- At least the five placeholder links are present and tappable:
  - Rust Book, GitHub, LinkedIn, Sentry (highlighted), Slides (pinned)
- Includes sections: Quick links, About the talk, About the speaker.
- Dark mode adapts automatically via `prefers-color-scheme`.
- Works without console errors; Lighthouse scores: A11y ≥ 95, SEO ≥ 90.

### Optional Enhancements (nice-to-have)

- Add icons (small inline SVG) beside each link type.
- Add copy-to-clipboard button for the slides URL.
- Generate a QR code image linking to the site for slide embedding.
- Basic analytics (privacy-friendly), e.g., Plausible/Umami.
- Service Worker for offline cache of `links.json` and `index.html`.

### Next Actions (for the agent)

1. Scaffold directories and files as above.
2. Paste the HTML, CSS, and JS starters and commit.
3. Populate `data/links.json` with placeholders provided here.
4. Test locally, then enable GitHub Pages and verify the live URL.
5. Hand off a short update note explaining how to add links going forward.
