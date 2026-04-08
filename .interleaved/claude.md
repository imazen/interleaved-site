# Interleaved Site — Instructions for Code Agents

This is the landing page for interleaved.org, built with Interleaved's
own Handlebars renderer as a dogfood project.

## Structure

- `templates/` — Handlebars HTML templates (partials prefixed with `_`)
- `content/` — Markdown pages with YAML frontmatter
- `data/site.json` — Global site data (name, URLs, tagline)
- `static/` — Copied as-is (favicon, images)

## Building

```bash
cd /path/to/interleaved
npx tsx scripts/build-site.ts --src /path/to/interleaved-site --out ./_site
```

## Deploying

```bash
npx wrangler pages deploy ./_site --project-name interleaved-site
```

## Adding pages

Create a markdown file in `content/`:
```markdown
---
title: Page Title
layout: base
description: One-line summary
---

Page content in markdown.
```

The `layout` field selects which template renders the page.
Available layouts: `base`, `index`.
