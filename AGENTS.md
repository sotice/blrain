# AGENTS.md — The Digital Diarist

## Project structure

```
thedigitaldiarist/          # Neocities site root
├── index.html              # Homepage (single-page site)
├── style.css               # All styles (monolithic, no preprocessor)
└── elements/               # Static assets (images, fonts, favicon)
```

- **No build step, no dependencies, no package manager.**
- Sub-pages (`/about`, `/reading`, etc.) linked in nav but not in this repo — they live on Neocities.
- Blog is hosted externally at `thedigitaldiarist.bearblog.dev`.

## Local development

Open `thedigitaldiarist/index.html` in a browser, or serve with any static file server:

```powershell
npx serve thedigitaldiarist
```

## Deployment

Upload contents of `thedigitaldiarist/` to [Neocities](https://neocities.org). No build step — files upload as-is.

## Notes

- No JavaScript on the site.
- Fonts are dual-sourced: Google Fonts CDN (Fraunces) + local WOFF in `/elements/googlefonts/`.
- RSS feed at `thedigitaldiarist.neocities.org/feed.xml` (hosted on Neocities, not in repo).
- The `elements/favicon/` directory is empty (placeholder for future favicons).
