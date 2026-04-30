# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

A personal static-file notes site hosted on GitHub Pages at `https://miyazawa-ron.github.io/my-notes/`. There is no build system, no package manager, and no test suite — all content is plain HTML and Markdown, committed and pushed directly.

## Content Structure

| File | Role |
|---|---|
| `index.html` | Navigation homepage — card grid linking to all notes |
| `_sidebar.md` | Sidebar nav (used if a Docsify-style viewer is layered on top) |
| `README.md` | GitHub repo overview; mirrors the index card list |
| `*.html` | Individual note pages (self-contained, no shared CSS file) |
| `*.md` | Markdown notes (rendered by GitHub or a viewer) |

## HTML Conventions

All note pages and the index share a **dark-theme CSS variable system** defined inline in each file's `<style>` block:

```css
:root {
  --bg: #0f0f13;
  --surface: #16161d;
  --surface2: #1e1e28;
  --border: #2a2a38;
  --accent: #e8c96d;       /* gold — primary highlight */
  --accent2: #7eb8c9;      /* blue — secondary */
  --text: #e8e4d8;
  --muted: #6b6880;
  --tag-jp: #c47b5a;
  --tag-grammar: #7eb8c9;
  --tag-vocab: #9bc47a;
}
```

Fonts loaded from Google Fonts: `Noto Serif JP` (headings/Japanese text), `Noto Sans SC` (body/Chinese text), `DM Mono` (monospace labels/code).

Each note page is fully self-contained — styles are embedded in `<style>` tags, no external stylesheet is shared across pages.

## Adding a New Note

1. Create a new `<name>.html` file following the existing dark-theme inline-CSS pattern.
2. Add a `<a class="card" href="<name>.html">` entry inside the `<div class="cards">` grid in `index.html` (before the `.card-add` placeholder).
3. Add a line to `_sidebar.md` under the appropriate category.
4. Add a row to the table in `README.md`.

## Deploying

Push to the `main` branch — GitHub Pages serves the repo root automatically. No build step required.
