# diogen.md

Marketing website for Diogen, a young Moldovan team offering web development,
custom software, business process digitization, IT consulting, and systems
integration services.

Built on top of UIdeck's open-source "Startup Template" (Bootstrap 5, MIT
licensed — see `LICENCE`). No backend, no build system, no package manager —
pages are plain `.html` files referencing shared assets in `assets/`.

## Site structure

- Romanian (primary market) is served at the domain root: `index.html`,
  `despre.html`, `contact.html`, `404.html`.
- English and Russian are full static copies under `en/` and `ru/`, using
  `index.html`, `about.html`, `contact.html`, `404.html`.
- Every page links to its equivalent in the other two locales via the
  language switcher in the header and footer.
- There is no templating engine, so shared markup (header/nav, footer, meta
  tags) is duplicated across every page and every locale. When changing
  shared UI, grep across all `.html` files (root and `en/`/`ru/`) and update
  each one.

## 🖥️ Local Development

This is a static HTML/CSS/JS site with no build step and no package manager.
To preview changes locally, serve the repo root with any static file server
(opening the files directly via `file://` also mostly works, but a server
avoids path/CORS quirks).

**Using Python (no install needed on most systems):**

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000/index.html in a browser (or
`/en/index.html`, `/ru/index.html` for the other locales).

**Using Node (if you have `npx` available):**

```bash
npx http-server -p 8000
```

To stop the server, press `Ctrl+C` in the terminal running it (or, if started
in the background, find and kill the process: `pkill -f "http.server 8000"`).

If you edit `assets/scss/*.scss`, you must compile it to
`assets/css/ud-styles.css` yourself (e.g.
`sass assets/scss/ud-styles.scss assets/css/ud-styles.css`) and commit both —
nothing watches or rebuilds SCSS automatically.

## 📃 License

Based on UIdeck's Startup Template, MIT licensed — see `LICENCE`.
