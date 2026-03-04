# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Academic personal website for Mitali Roy Mathur, built with Jekyll using the [al-folio](https://github.com/alshedivat/al-folio) theme. Deployed to GitHub Pages at mitali-mathur.github.io.

## Build & Development Commands

```bash
# Install dependencies
bundle install

# Local development server
bundle exec jekyll serve

# Production build (matches CI)
JEKYLL_ENV=production bundle exec jekyll build

# Build output goes to _site/
```

CI/CD (`.github/workflows/deploy.yml`) runs on push to master: installs Ruby 3.2.2, Jupyter, mermaid.cli, then builds and deploys `_site/` to GitHub Pages.

## Architecture

**Content collections:**
- `_pages/` — Static pages (about, cv, teaching, publications, projects)
- `_posts/` — Blog posts
- `_projects/` — Project cards (numbered, support categories via `category` front matter)
- `_news/` — Announcements (output disabled, shown inline on about page)
- `_bibliography/papers.bib` — Publications managed via Jekyll Scholar (BibTeX)
- `_data/` — Structured data: `cv.yml`, `coauthors.yml`, `repositories.yml`, `venues.yml`
- `assets/json/resume.json` — JSON Resume data loaded via `jekyll-get-json`

**Theme/layout system:**
- `_layouts/` — Liquid templates (about, page, post, cv, bib, distill, archive-*)
- `_includes/` — Partials (header, footer, social, scripts, cv/, resume/, repository/)
- `_sass/` — SCSS styles
- `_plugins/` — Custom Ruby plugins (cache-bust, details tag, external-posts, file-exists, hideCustomBibtex)

**Key config (`_config.yml`):**
- Jekyll Scholar configured with APA style, grouped by year descending
- `scholar.last_name`/`first_name` controls author highlighting — currently set to Einstein (template default), should be updated for the site owner
- ImageMagick generates responsive WebP images from `assets/img/`
- Feature flags: `enable_math`, `enable_darkmode`, `enable_masonry`, `enable_medium_zoom`, `enable_project_categories`, `enable_progressbar`

## Content Editing Patterns

- Blog posts: `_posts/YYYY-MM-DD-title.md` with standard Jekyll front matter
- Projects: `_projects/N_project.md` with `category` front matter for filtering
- Publications: edit `_bibliography/papers.bib`, rendered by Jekyll Scholar using `_layouts/bib.html`
- CV data: `_data/cv.yml` drives the CV page layout
- News items: `_news/announcement_N.md`

## Pre-commit Hooks

Configured in `.pre-commit-config.yaml`: trailing whitespace, end-of-file fixer, YAML validation, large file check (500KB).