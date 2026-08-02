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
npm run build         # Build production CSS (PurgeCSS) and JS (Rollup)
npm run watch:js      # Watch and rebuild JS in development
npm run lint:scss     # Lint SCSS files
npm run lint:fix:scss # Auto-fix SCSS lint issues
```

### Running tests

```bash
npm test              # Runs SCSS lint (the only automated test)
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

### Post Writing Standards

All posts follow a consistent structure and style. When creating or editing posts, respect these conventions:

**Structure:**
- Opening paragraph(s) with no heading — sets context and hooks the reader
- Sections marked with `## **Título da seção**` (bold inside the heading)
- Subsections marked with `### **Subtítulo**` and `#### **Sub-subtítulo**` when needed
- Short, focused paragraphs — one or two ideas per paragraph, never walls of text
- Paragraphs use `text-align: justify` via CSS — no manual line breaks needed

**Language and tone:**
- Written in Portuguese (pt-BR), informal but substantive
- Author's direct, opinionated voice — do not soften or genericize
- Technical terms in English are kept as-is (e.g., *trade-off*, *framework*, *debug*)

**Spelling rules to watch:**
- `algoritmos` — sem acento no "i" (not *algorítmos*)
- `videoaulas` — uma palavra só (not *vídeo-aulas*)
- `eletricistas` — sem acento no "é" (not *elétricistas*)
- Image paths must start with `/assets/img/...` (leading slash required)

### Cyberpunk-Minimalist Theme

The blog uses a custom cyberpunk-minimalist visual identity defined in `_sass/components/_cyberpunk.scss`. Key design decisions:

- **Primary color:** `#00ff00` (titles, active nav, h1)
- **Accent color:** `#00cc00` (h2, h3, h4, tags, links)
- **Body text:** `#c8c8d2` (cool off-white)
- **Font:** Space Grotesk (loaded via Google Fonts in `_includes/head.html`)
- No glow/text-shadow effects — pure flat color only
- `text-align: justify` on paragraph content for visual consistency

To change colors or typography, edit `_sass/components/_cyberpunk.scss` only. Do not touch the Chirpy theme files.

### Theme and Assets

The site uses the `jekyll-theme-chirpy` gem. Most layout files (`_layouts/`, `_includes/`) and base SCSS come from the gem and are **not** in this repo. Only overrides and additions live locally:

- `_sass/` — SCSS overrides and custom styles layered on top of the theme
- `_sass/components/_cyberpunk.scss` — all cyberpunk theme customizations
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
refactor: description
docs: description
chore: description
```
