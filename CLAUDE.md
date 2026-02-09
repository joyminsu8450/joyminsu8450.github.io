# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll blog site (`joyminsu8450.github.io`) using the **Plainwhite** theme (v0.13), a minimalist portfolio-style theme for writers. It is deployed via GitHub Pages.

## Build & Serve Commands

```bash
bundle install              # Install dependencies (from gemspec)
bundle exec jekyll serve    # Serve locally at http://localhost:4000 (live reload on changes)
bundle exec jekyll build    # Build static site to _site/
```

There are no test or lint commands — this is a pure Jekyll theme/site with no CI pipeline.

## Architecture

### Theme Structure (Plainwhite)

The site bundles the theme directly (not as a remote gem). All theme files are local and editable:

- **`_layouts/`** — Four layouts: `default.html` (main wrapper with sidebar + content), `home.html` (post listing + search), `post.html` (single post + Disqus), `page.html` (static page). All inherit from `default`.
- **`_includes/head.html`** — `<head>` tag: meta tags, Google Fonts (Merriweather, Raleway), compiled CSS link, jekyll-seo-tag, dark mode script injection.
- **`_sass/`** — `plain.scss` (main layout/typography), `dark.scss` (dark mode overrides), `search.scss`, `toggle.scss` (dark mode switch), `_syntax.scss` (code highlighting). Vendor styles in `ext/` (normalize, fonts, solarized themes).
- **`assets/js/`** — `darkmode.js` (cookie-based OS preference detection), `search.js` (Simple-Jekyll-Search integration), `simple-jekyll-search.min.js` (vendor lib).

### Configuration

All theme customization lives under the `plainwhite` key in `_config.yml`:
- `name`, `tagline`, `portfolio_image`, `social_links`, `navigation`
- Feature flags: `search`, `dark_mode`, `condensed_mobile`
- Integrations: `analytics_id` (Google Analytics), `disqus_shortname` (comments)

**Note:** `_config.yml` is currently deleted from the working tree and needs to be recreated for the site to build properly.

### Key Design Patterns

- **Two-column layout**: Fixed sidebar (`.about`, width `220px`) + scrollable content (`.content`). Collapses to single-column below `768px`.
- **SCSS breakpoints**: `$mobileW: 768px`, `$smallMobileW: 480px`, `$bigScreenW: 1600px`.
- **Dark mode**: Toggled via body class, persisted in cookies, auto-detects OS `prefers-color-scheme`. Solarized dark/light syntax themes swap accordingly.
- **Search**: Client-side via `search.json` (Liquid-generated index of all posts) + Simple-Jekyll-Search library.

### Content

- Blog posts go in `_posts/` using `YYYY-MM-DD-title.markdown` naming convention.
- Static pages (e.g., `about.markdown`, `index.md`) live at the root.
- `search.json` and `sitemap.xml` are Liquid templates that auto-generate from post data.

### Gem Dependencies

Defined in `plainwhite.gemspec` (Gemfile just references gemspec):
- `jekyll` (>= 3.7.3)
- `jekyll-seo-tag` (>= 2.1.0)
