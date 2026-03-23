# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Install dependencies
bundle install

# Run local dev server (http://localhost:4000)
bundle exec jekyll serve

# Build site
bundle exec jekyll build
```

The site auto-deploys to GitHub Pages on every push to `main` via `.github/workflows/jekyll-gh-pages.yml`.

## Architecture

This is a Jekyll site using the "Mria" theme, built for **Red Rover** — a camping vacation booking service.

### Configuration

- **`_config.yml`** — Jekyll build settings: markdown engine, permalink structure, plugins, collection definitions, and Sass config. Rarely changed.
- **`_data/settings.yml`** — The primary site content config: site title/logo, navigation menus, hero section, section toggles (blog, videos, tags, author, newsletter), social links, footer content, Formspree contact email, Disqus shortname, and Google Analytics ID. Most content/feature changes start here.

### Collections

- **`_posts/`** — Blog posts (markdown, date-prefixed filenames)
- **`_pages/`** — Static pages (about, contact, tags, authors)
- **`_authors/`** — Author profiles; each file generates an author page

### Templates & Includes

- **`_layouts/`** — Four layouts: `default` (wraps all pages), `page`, `post`, `author`
- **`_includes/`** — Reusable partials. Homepage sections are prefixed `section-*` (e.g., `section-hero.html`, `section-blog.html`, `section-videos.html`). Each section can be enabled/disabled via `_data/settings.yml`.

### Styling

SCSS entry point is `_includes/main.scss`, which imports everything in layer order:

```
0-settings/  → variables, color-scheme (CSS custom props), mixins, helpers
1-tools/     → normalize, reset, grid, animations, syntax highlighting
2-base/      → base element styles
3-modules/   → header, footer, hero, article, search, sections, etc.
4-layouts/   → post page, authors page, tags page
```

Dark/light mode is implemented via CSS custom properties on `:root` vs `:root[dark]`. The `color_scheme` in `_data/settings.yml` can be `auto`, `light`, or `dark`.

### JavaScript

`js/scripts.js` and `js/common.js` are loaded in `_layouts/default.html`. No build step — vanilla JS only, no jQuery.
