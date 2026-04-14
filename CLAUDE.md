# CLAUDE.md — my-notes

## Project Overview

**my-notes** is a personal Japanese language learning notes repository hosted on GitHub Pages. It targets Chinese speakers studying Japanese for JLPT N4 → N2.

- **Live site**: https://miyazawa-ron.github.io/my-notes/
- **Primary audience**: Chinese speakers (UI text in Simplified Chinese, content in Japanese)
- **Goal**: Structured JLPT study notes progressing N5 → N4 → N3 → N2

---

## Repository Structure

```
my-notes/
├── index.html                  # Hub/navigation page (dark theme, card grid)
├── japanese_hours_1.html       # 24-hour time expressions (N4-N5 vocabulary)
├── n5_n4_grammar_reference.html # N5/N4 grammar reference (tabbed, JS-filtered)
├── README.md                   # GitHub repo overview with note directory table
└── _sidebar.md                 # Docsify-style sidebar (legacy, not actively used)
```

### File Roles

| File | Purpose |
|---|---|
| `index.html` | Central navigation hub. Lists all note files as clickable cards. **Update this when adding a new note.** |
| `japanese_hours_1.html` | Self-contained vocabulary reference for 24-hour time in Japanese |
| `n5_n4_grammar_reference.html` | Grammar reference with tab-based filtering (助词, 动词, 句型, 时态, N4重点) |
| `README.md` | Shown on GitHub repo page. Has a table of all notes and a roadmap checklist |
| `_sidebar.md` | Sidebar definition (retained but minimal; not used by GitHub Pages) |

---

## Tech Stack

- **Pure static HTML/CSS/JS** — no build system, no package manager, no frameworks
- **Google Fonts** (loaded from CDN):
  - `Noto Serif JP` — Japanese serif headings
  - `Noto Sans SC` — Chinese sans-serif body text
  - `DM Mono` — monospace labels and metadata
- **Hosting**: GitHub Pages (deploys automatically from `main` branch)
- **No compilation step** — files are deployed as-is

---

## Design System

### index.html — Dark Hub Theme

CSS custom properties defined in `:root`:

```css
--bg: #0f0f13          /* page background */
--surface: #16161d     /* card background */
--surface2: #1e1e28    /* card hover background */
--border: #2a2a38      /* borders */
--accent: #e8c96d      /* gold accent (hover highlights, headings) */
--accent2: #7eb8c9     /* secondary accent (unused in current cards) */
--text: #e8e4d8        /* primary text */
--muted: #6b6880       /* secondary/muted text */
--tag-jp: #c47b5a      /* tag: Japanese content */
--tag-grammar: #7eb8c9 /* tag: grammar category */
--tag-vocab: #9bc47a   /* tag: vocabulary category */
```

Tag classes: `.tag.jp`, `.tag.gram`, `.tag.voc`

Cards use `fadeUp` keyframe animation with staggered `animation-delay` per `.card:nth-child(n)`.

### Individual Note Pages — Light Theme

`japanese_hours_1.html` uses a light paper aesthetic:
```css
--paper: #f5f0e8   /* warm off-white background */
--ink: #1a1a2e     /* dark ink color */
--red: #c0392b     /* special/irregular entries */
--gold: #b8860b    /* accent */
```

`n5_n4_grammar_reference.html` uses a minimal system-font light theme (`#f5f5f0` background, `#1a1a1a` text) with JavaScript-driven tab filtering via `onclick="show('category')"`.

---

## Conventions

### Adding a New Note

1. **Create the HTML file** — name it descriptively (e.g., `n3_vocabulary_week1.html`). Model the structure on an existing note file.
2. **Add a card to `index.html`** — copy an existing `<a class="card" href="...">` block inside `<div class="cards" id="cards">`, placed before the `.card-add` placeholder:
   ```html
   <a class="card" href="your-file.html">
     <span class="card-icon">📝</span>
     <div class="card-title">Note Title in Japanese</div>
     <div class="card-sub">your-file.html</div>
     <div class="card-tags">
       <span class="tag jp">日本語</span>
       <span class="tag gram">文法</span>   <!-- or .voc for vocabulary -->
       <span class="tag gram">N3</span>
     </div>
     <span class="card-arrow">↗</span>
   </a>
   ```
3. **Update `README.md`** — add a row to the `## 📚 笔记目录` table:
   ```md
   | [Note Title](https://miyazawa-ron.github.io/my-notes/your-file.html) | Brief description | 分类 Level |
   ```
4. Update the roadmap checklist in `README.md` if a level milestone is completed.

### HTML Note File Conventions

- `lang="zh"` on `<html>` (UI is Chinese)
- `charset="UTF-8"` always
- Self-contained: all CSS is inline in `<style>` tags, no external CSS files
- JavaScript (if needed) is inline at the bottom of `<body>`
- Include a back-link to `index.html`: `<a href="index.html">← 返回导航首页</a>`
- Google Fonts are loaded via `<link>` in `<head>`

### Tag Guidelines

| Tag class | Use for |
|---|---|
| `.tag.jp` | Marks content as Japanese language material |
| `.tag.gram` | Grammar patterns, sentence structures |
| `.tag.voc` | Vocabulary, word lists, expressions |

JLPT level tags (N5, N4, N3, N2) use `.tag.gram` or `.tag.voc` class as appropriate.

---

## Development Workflow

- **No local build needed** — open any `.html` file directly in a browser to preview
- **Deployment** — push to `main` branch; GitHub Pages serves automatically
- **Editing** — files are self-contained and can be edited directly; historically uploaded via GitHub web UI ("Add files via upload" commits)
- **No linting or test suite** — validate by opening in browser

---

## Content Conventions

- **UI language**: Simplified Chinese (菜单、标签、说明)
- **Study content**: Japanese (kanji, kana, romaji as needed)
- **Translation notes**: Chinese translations of Japanese examples
- **JLPT levels**: N5 is beginner (currently complete), progressing toward N2
- **Grammar card structure** (in `n5_n4_grammar_reference.html`):
  - `pattern` — the grammar form (e.g., `〜てもいい`)
  - `meaning` — Chinese explanation
  - `ex` — Japanese example sentence
  - `zh` — Chinese translation of the example

---

## GitHub Pages Configuration

- Served from the root of `main` branch
- `index.html` at root is the entry point
- No Jekyll, no `_config.yml` — plain static files only
- `_sidebar.md` is not processed by GitHub Pages (would require Docsify setup)
