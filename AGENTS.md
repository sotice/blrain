# AGENTS.md — 数字日记

## Project structure

```
digitaldiarist/             # Repository root (= Neocities site root)
├── index.html              # Homepage
├── style.css               # All styles (monolithic, no preprocessor)
├── about/                  # 关于
│   └── index.html
├── reading/                # 阅读
│   └── index.html
├── watching/               # 观影
│   └── index.html
├── listening/              # 音乐
│   └── index.html
├── writing/                # 写作
│   └── index.html
└── elements/               # Static assets
    ├── logo/               # Brand / header image
    ├── img/                # Content images
    ├── patterns/           # Background textures
    └── favicon/            # Empty (placeholder for favicons)
```

- **No build step, no dependencies, no package manager.**
- Each section is a folder containing an `index.html` — open `/reading/` to read the reading page, etc.
- Sub-pages inside sections (e.g. `/reading/journal/2025/`, `/reading/e-lit/`) referenced in `index.html` do not exist yet — placeholders only.

## Local development

Open `index.html` in a browser, or serve the repo root with any static file server:

```powershell
npx serve .
```

## Deployment

Upload the entire repository root to [Neocities](https://neocities.org). No build step — files upload as-is.

## Notes

- No JavaScript on the site.
- Fonts are dual-sourced: Google Fonts CDN (Fraunces, Noto Serif SC) + local WOFF fallbacks in `/elements/googlefonts/` and `/elements/handwrittenfonts/` (these fallback directories are referenced by `style.css` but not yet in the repo).
- RSS feed at `thedigitaldiarist.neocities.org/feed.xml` (hosted on Neocities, not in repo).
- `elements/favicon/` is empty — placeholder for future favicons.
