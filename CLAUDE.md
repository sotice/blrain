# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

This is a pure static-site personal blog ("The Digital Diarist" / 随笔) — no frameworks, no build step, no package manager. A single shared CSS file (`style.css`) and flat HTML pages organized into subject directories. The site is written in Simplified Chinese.

## Development

There is no build tooling, test runner, or linter. To preview the site, serve the repository root with any static HTTP server:

```bash
npx serve .          # Node-based, or:
python -m http.server 8080
```

Open `http://localhost:<port>` — the browser loads `index.html` directly.

## Architecture

### Page structure

Each top-level section lives in its own directory and contains an `index.html`:

| Directory | Page |
|---|---|
| `/` | Homepage (recent entries) |
| `reading/` | Reading journal, book club, e-lit |
| `watching/` | Film/TV log |
| `listening/` | Music & podcasts |
| `writing/` | Writing projects & dynamically-loaded Markdown posts |
| `about/` | About the author (blrain) |

Every page follows the same shell: `<head>` with meta tags (charset, viewport, OG) → Google Fonts stylesheet → link to `style.css` → `<body>` with `<div class="siteheader">` (logo + nav) → `<main>` content.

Subdirectory pages (`about/`, `reading/`, etc.) reference `../style.css` and use `../` paths for navigation links and assets. The root `index.html` uses `style.css` and bare relative paths (e.g., `elements/logo/...`).

### Navigation

The sticky site header is duplicated across every page. The nav links are:

```
书籍 (reading/) → 观影 (watching/) → 音乐 (listening/) → 写作 (writing/) → 关于 (about/)
```

When adding a new section, update the nav in all six `index.html` files.

### CSS (`style.css`)

- Single shared stylesheet for the entire site
- Dark theme ("nocturnal copper"): background `#1a1f2e`, text `#c5c2b8`, accent `#c87944` (copper/orange), secondary `#7a8da6` (blue-grey)
- Custom fonts via `@font-face` (Fraunces, Minion Pro, Meera Inimai, Homemade Apple, Deneane, Ukulele Setlist) — self-hosted WOFF files in `elements/googlefonts/` and `elements/handwrittenfonts/`
- Google Fonts CDN used as fallback for Fraunces, Homemade Apple, Meera Inimai, and Noto Serif SC (for CJK)
- Layout: 60% width `<main>`, flexbox-based `.flex`/`.flexreverse` rows, `.window` bordered boxes with sticky headers
- Responsive breakpoints: 1024px (75% width), 780px (75% width, stacked flex), 480px (90% width)
- Reusable accent boxes: `.redbox`, `.greenbox`, `.goldbox`
- Custom scrollbar styling (WebKit only)

### Writing section — Markdown posts

The writing page (`writing/index.html`) loads Markdown posts dynamically via `marked.js` loaded from CDN. To add a post:

1. Add a `.md` file to `writing/posts/`
2. Register it in the `posts` array in `writing/index.html`:
   ```js
   const posts = [
     { file: "posts/example.md", title: "范文：标题" },
     { file: "posts/my-new-post.md", title: "我的新随笔" },
   ];
   ```

The script fetches each file, parses it with `marked.parse()`, and injects the HTML into `<div id="posts">`.

### Assets

- `elements/logo/` — site logo (used in site header)
- `elements/img/` — article images
- `elements/patterns/` — background texture (`rice-paper-2.png`)
- `elements/favicon/` — favicon files
- `elements/googlefonts/` — self-hosted WOFF font files
- `elements/handwrittenfonts/` — additional self-hosted fonts

### Key conventions

- Language: all content in Simplified Chinese (`lang="zh-CN"`)
- Custom HTML elements: `<date>` for post dates (styled in CSS), `<cite>` for work titles
- No-cache meta tags on the homepage (`no-cache, no-store, must-revalidate`)
- Navigation links use trailing slash directory paths (e.g., `href="reading/"`)
- OG and Twitter card meta tags on most pages for link previews
