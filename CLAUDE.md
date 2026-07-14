# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

This is the **deploy target only** — GitHub Pages repo for `leonardoborges.com` (see `CNAME`). It is not where the site is authored. Do not hand-edit `index.html`, `about.html`, `books.html`, `contact.html`, `404.html`, or anything under `_next/` — those are Next.js static-export output and will be overwritten (and diverge from source) if edited here directly.

## Where the real source is

The current source is `/Users/leoborges/projects/leadtech-diet` (misleadingly named directory — it's the personal site, not a diet app; git remote is `theleoborges/leoborges_minisite.git`). It's a Next.js 15 app with `output: 'export'` in `next.config.ts`.

To make a change:
1. Edit in `leadtech-diet` (pages under `app/`, static assets under `public/`).
2. `cd leadtech-diet && npm run build` — static export lands in `leadtech-diet/out/`.
3. Sync into this repo: `rsync -a --exclude='.git' leadtech-diet/out/ leonardoborges.github.io/` — **no `--delete`** (see below).
4. Commit and push from here.

## Legacy Hugo content — do not delete

`/Users/leoborges/projects/leonardoborges.com` (Hugo) used to be the site source and is now stale/superseded for the pages Next.js has taken over (home, about, books, contact, 404). But this repo's `writings/`, `post/`, `tags/`, `categories/`, `talks/`, `projects/`, `ananke/`, `index.xml`, `sitemap.xml` directories are still old Hugo-generated output that the Next.js migration hasn't replaced. They are not present in `leadtech-diet/out/`, so a plain rsync (without `--delete`) leaves them alone — keep it that way.

## Static assets / one-off pages

Self-contained HTML files or standalone visualizations (e.g. `/for-the-love-of-writing/`) are added under `leadtech-diet/public/<path>/` (served verbatim at that path by Next.js), then flow through the build/sync steps above like any other change.
