# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is Stefan Girstmair's personal academic website, built with Jekyll using the [academicpages](https://github.com/academicpages/academicpages.github.io) template (a fork of Minimal Mistakes). It is deployed via GitHub Pages at https://stefangirstmair.github.io/.

## Local Development

```bash
# Install dependencies (one-time)
sudo apt install ruby-dev ruby-bundler nodejs
bundle install

# Serve locally with live reload (recommended)
bundle exec jekyll liveserve

# Serve with dev config (disables analytics, uses localhost URL)
bundle exec jekyll serve --config _config.yml,_config.dev.yml
```

The site is available at `http://localhost:4000`. Jekyll watches for file changes and rebuilds automatically.

If you get bundle errors, delete `Gemfile.lock` and re-run `bundle install`.

## Site Architecture

Content lives in Jekyll collections and pages — all written in Markdown with YAML front matter.

**Key collections** (each item = one `.md` file):
- `_publications/` — research papers; uses custom front matter (`paperurl`, `subtitle`)
- `_talks/` — conference talks and presentations
- `_teaching/` — teaching positions
- `_pages/` — standalone pages served at fixed permalinks

**Primary content files for this site:**
- `_pages/about.md` — homepage (permalink: `/`)
- `_pages/research.md` — research page with full paper descriptions (this is the main research page, not `_publications/`)
- `_pages/cv.md` — CV page
- `_pages/teachingmd.md` — teaching page
- `_data/navigation.yml` — top navigation bar links
- `_config.yml` — site-wide settings (author info, social links, analytics)
- `files/` — PDFs and downloadable files (e.g., `CV_Girstmair.pdf`)

**Layouts** (in `_layouts/`):
- `talk.html` — used by all `_talks/` entries
- `single.html` — used by pages, posts, publications, teaching
- `default.html` — base layout

**Navigation** is controlled entirely by `_data/navigation.yml`. Items can be commented out to hide them from the menu.

## Content Conventions

**Publications front matter:**
```yaml
---
title: "Paper Title"
subtitle: "Job Market Paper"   # optional label
collection: publications
excerpt: 'Abstract text here'
paperurl: 'http://stefangirstmair.github.io/files/paper.pdf'
---
```

**Talks front matter:**
```yaml
---
title: "Talk Title"
collection: talks
type: "Conference talk"
permalink: /talks/YYYY-MM-DD-slug
venue: "Conference Name"
date: YYYY-MM-DD
location: "City, Country"
---
```

**The `_pages/research.md` file** is the primary research page shown in navigation — it contains full paper descriptions written manually. The `_publications/` collection is a secondary mechanism (not currently linked in nav).

## Markdown Generator

`markdown_generator/` contains Python scripts and Jupyter notebooks to batch-generate talk/publication markdown files from TSV spreadsheets (`talks.tsv`, `publications.tsv`). Use these if adding many entries at once.

## Deployment

Pushing to the `master` branch automatically triggers GitHub Pages to rebuild and deploy the site. There is no CI/CD pipeline to configure.
