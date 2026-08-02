# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal blog called **Código 404** built with Jekyll using the [Chirpy theme](https://github.com/cotes2020/jekyll-theme-chirpy). It is hosted on GitHub Pages at `https://rafaelrodriguest.github.io/blog-codigos-brisas`. The blog covers programming, technology, and career topics, written in Portuguese (pt-BR).

## Commands

### Jekyll (Ruby) — serving and building the site

```bash
bundle exec jekyll serve          # Start local dev server at http://127.0.0.1:4000
bundle exec jekyll serve --drafts # Include draft posts
bundle exec jekyll build          # Build to _site/
```

### Node.js — JS/CSS assets

```bash
npm run build        # Build production CSS (PurgeCSS) and JS (Rollup)
npm run watch:js     # Watch and rebuild JS in development
npm run lint:scss    # Lint SCSS files
npm run lint:fix:scss # Auto-fix SCSS lint issues
```

### Running tests

```bash
npm test             # Runs SCSS lint (the only automated test)
```

## Architecture

### Content

- `_posts/` — blog posts in Markdown. Filename format: `YYYY-MM-DD-slug.md`
- `_drafts/` — unpublished drafts (not committed to git normally)
- `_tabs/` — static pages rendered as sidebar tabs (About, Archives, Categories, Tags)

### Post Front Matter

Every post requires:

```yaml
---
layout: post
title: 'Post Title'
date: YYYY-MM-DD HH:MM:SS -0300
categories: [Category, Subcategory]
tags: [tag1, tag2]
---
```

Optional front matter: `image:` (social preview), `pin: true` (pin to homepage), `toc: false` (disable table of contents).

### Theme and Assets

The site uses the `jekyll-theme-chirpy` gem. Most layout files (`_layouts/`, `_includes/`) and base SCSS come from the gem and are **not** in this repo. Only overrides and additions live locally:

- `_sass/` — SCSS overrides and custom styles layered on top of the theme
- `_javascript/` — custom JS modules bundled with Rollup
- `assets/` — images and compiled output (`assets/js/dist/`, `assets/css/`)
- `_data/` — theme data files (localization, contact links, share buttons)

### Configuration

`_config.yml` is the main configuration. Key settings:
- `lang: pt-BR`, `timezone: America/Sao_Paulo`
- `baseurl: ""` — served from root
- `permalink: /posts/:title/` — post URL pattern
- `paginate: 10`
- Comments, analytics, and PWA providers are configured in `_config.yml` but currently disabled (empty values)

### Commit Convention

This project uses **Conventional Commits** enforced by commitlint + husky:

```
feat: description
fix: description
docs: description
chore: description
```
