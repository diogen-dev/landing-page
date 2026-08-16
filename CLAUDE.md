# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static HTML/CSS/JS marketing site (Bootstrap 5) for **diogen.md** — a young Moldovan team offering web development, custom software, business process digitization, IT consulting, and systems integration. Built on top of UIdeck's "Startup Template". No backend, no build system, no package manager, no test suite — pages are plain `.html` files that reference shared assets in `assets/`. See `DECISIONS.md` for the rebrand decision log (scope, what was dropped, what's still deferred).

## Development

There is no build step and no local server tooling checked into the repo. To preview, open the HTML files directly in a browser or serve the directory with any static file server (e.g. `python3 -m http.server`).

CSS is authored in SCSS under `assets/scss/` but the compiled output (`assets/css/ud-styles.css` + `.css.map`) is committed directly — there is no SCSS compiler config (no `package.json`, gulpfile, etc.) in this repo. If you edit `assets/scss/*.scss`, you must compile it to `assets/css/ud-styles.css` yourself (e.g. via `sass assets/scss/ud-styles.scss assets/css/ud-styles.css`) and commit both, since nothing else will pick up SCSS-only changes. If no `sass` compiler is available in your environment, hand-edit `ud-styles.css` to match the `.scss` change and note that `.css.map` is now stale rather than silently leaving the two out of sync.

## Architecture

- **Locales**: three full static copies, no JS toggle, no shared templating.
  - Romanian is the primary market language and is served at the domain root: `index.html`, `despre.html`, `contact.html`, `404.html`.
  - English and Russian each live in their own subfolder — `en/` and `ru/` — using `index.html`, `about.html`, `contact.html`, `404.html`.
  - Every page carries a language switcher (header nav + footer) linking to its equivalent page in the other two locale trees. When adding/renaming a page or anchor, update the switcher links on all three locale variants.
- Each `.html` file is a standalone page — there is no templating engine, so shared markup (header/nav, footer, meta tags) is duplicated across every page *and* every locale. When changing shared UI (nav, footer, etc.), grep across all `.html` files (root and `en/`/`ru/`) and update each one.
- Page set is intentionally small: `index` (home), `about` (despre.html in RO), `contact`, `404` — per locale. `login.html`, `pricing.html`, `blog.html`, and `blog-details.html` from the original template were dropped entirely (see `DECISIONS.md`).
- `assets/scss/` is partitioned per-page/section (`_header.scss`, `_hero.scss`, `_footer.scss`, `_404.scss`, etc.) and assembled by `assets/scss/ud-styles.scss` via `@import`. `_variables.scss` and `_mixin.scss` hold shared tokens/mixins; `_common.scss` holds cross-page base styles. `_pricing.scss`, `_login.scss`, and `_blog.scss` are unused leftovers from the template (not imported by any kept page) and can be removed if the corresponding page types never return.
- `assets/js/main.js` is the only custom script (sticky header, mobile nav toggle, back-to-top button); `bootstrap.bundle.min.js` and `wow.min.js` (scroll animations, paired with `animate.css`) are vendored third-party libs.
- `assets/images/` and `assets/fonts/` hold static media and the LineIcons icon font referenced via `assets/css/lineicons.css`. Team-photo, testimonial-avatar, and partner-brand-logo images from the original template are no longer referenced by any page (team/testimonials sections were replaced with prose or dropped) but haven't been deleted from `assets/`.
- `CNAME` points to `diogen.md`; the site is deployed via GitHub Pages with a custom domain.
- The logo is a plain CSS-styled text wordmark (`<span class="fw-bold text-white ud-logo-text">Diogen</span>`), not an image — swap in a real logo file later without touching markup structure beyond that one element, repeated in every page's header and footer.
- Contact details (email, city) are clearly-fake placeholders marked with an HTML comment (`<!-- TODO: replace placeholder contact details -->`) above the contact info block on every `contact.html`/`contact` section; the contact form has no backend wiring.
