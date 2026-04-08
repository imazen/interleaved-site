---
title: How It Works
layout: base
description: The architecture behind Interleaved — how human content editing and AI code generation share the same git repo.
---

# How Interleaved Works

Interleaved is a CMS that lives between you and your git repo. You edit content on your phone. Claude edits templates and code. Both commit to the same repository.

## The Architecture

```
You (phone/desktop)        Claude (terminal)
    │                          │
    │  edit content             │  edit templates
    │  upload media             │  edit styles
    │  preview changes          │  refactor code
    │                          │
    ▼                          ▼
┌─────────────────────────────────┐
│         Git Repository          │
│  content/*.md   templates/*.html│
│  data/*.json    static/         │
└─────────────────────────────────┘
    │                          │
    ▼                          ▼
  Build                    Build
  (same pipeline, triggered by either)
    │
    ▼
  Live Site
```

## No Schema Required

Most CMS tools make you define your content model before you can start editing. Interleaved doesn't.

Drop markdown files in a repo. Interleaved scans them, reads the frontmatter, and infers field types. Dates look like dates. Booleans look like booleans. Images get image pickers. Tags get tag editors.

If you want explicit control, add a `.pages.yml` or `.interleaved/config.json`. But you don't have to.

## Works With Any Generator

Interleaved doesn't build your site. It edits files. Your existing build pipeline handles the rest.

- **Astro** — content collections work directly
- **Hugo** — `content/` and `data/` auto-detected
- **Eleventy** — `src/` structures supported
- **Next.js** — markdown in any directory
- **Built-in** — Handlebars templates, no framework needed

Or anything else that reads files from git.

## Media Without Git Bloat

User-uploaded images go to Cloudflare R2, not your git repo. Each repo gets an isolated storage namespace.

Images support query-string transforms for responsive delivery:

```
hero.jpg?w=800&format=webp
hero.jpg?w=400&h=300&mode=crop
```

Theme assets (logos, icons) stay in git. User content (photos, uploads) goes to blob storage.

## Two Workflows

**Direct** (default): Every edit commits straight to your default branch. Site rebuilds immediately. Good for personal sites and small teams.

**Branch**: Edits go to a draft branch. Preview through your deploy platform. Click "Publish" to create a PR or merge. Good for production sites with review processes.

## Open Source

Interleaved is MIT licensed. Fork it, self-host it, modify it. The codebase is a fork of [Pages CMS](https://github.com/pagescms/pagescms), rebuilt for mobile-first editing and AI integration.

[Get started](https://interleaved.app) or [view the source](https://github.com/imazen/interleaved).
