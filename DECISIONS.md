# Diogen.md — Rebrand Decision Log

Decisions made while adapting the "Startup Template" (UIdeck) into the
diogen.md website. This is the source of truth for scope until superseded.

## Identity & Domain

- **Domain**: `diogen.md` (literal, Moldova ccTLD). `CNAME` must be updated
  from the template's `startup.hau.xyz` to `diogen.md`.
- **Who**: A young team of specialists providing digitization / custom IT
  solutions to companies in Moldova.
- **Branding**: No real brand assets exist yet.
  - Logo: placeholder text wordmark ("Diogen"), CSS-styled, replacing the
    template's SVG logo files — swappable later without touching markup.
  - Color palette: keep the template's existing Bootstrap purple/blue theme
    as-is for now (no palette redesign).
- **Contact details**: no real email/phone/address yet — use clearly-fake
  placeholders (e.g. `hello@diogen.md`) marked for later replacement.
- **Contact form**: leave `contact.html`'s form non-functional (no backend/
  form-service wiring) for now.

## Languages & Site Structure

- **Languages**: Romanian, English, Russian — all three shipped, not phased.
- **Architecture**: full static copy per locale (no JS toggle, no shared
  templating). `/en/` and `/ru/` subfolders, each a complete page set.
- **Root**: `diogen.md/` root *is* the Romanian site directly (`index.html`
  at root = RO). Romanian is primary market language, gets the bare URL.
- **Language switcher**: yes, nav/footer link across the three locale trees
  to the equivalent page (e.g. RO `/despre.html` ↔ EN `/en/about.html`).
- **Page set**: follow the template's existing pages/sections, minus the
  ones explicitly dropped below. No new pages invented (no dedicated
  Services or Portfolio page) — content lives in the homepage sections.
  Kept: `index`, `about`, `contact`, `404` (× 3 locales).
- **Dropped entirely**: `login.html`, `pricing.html` (both the standalone
  page and the inline pricing section embedded in `index.html`),
  `blog.html`, `blog-details.html`.

## Homepage / About Section Changes

- **Features section**: repurpose the 4-item grid for the services list:
  web development, custom software, business process digitization, IT
  consulting, systems integration. (5 services vs. 4 template slots — needs
  a layout tweak when implemented.)
- **Testimonials section**: removed entirely (no real clients yet as a new
  venture; no placeholder quotes).
- **Team section**: replace the 4-photo/name card grid with prose narrative
  — generic "young team of specialists" copy, no individual names, roles,
  or photos.
- **FAQ section**: keep. Content to be (re)written for an IT-services
  engagement context — process, timelines, pricing model, tech stack —
  rather than the template's generic SaaS FAQ.

## Not Yet Decided / Explicitly Deferred

- Exact service-page copy tone/length, FAQ question set — to be drafted.
- Real contact info, real logo/brand palette — swap in once available.
- Whether/when to bring back a Portfolio/case-studies section (deferred
  until there are real projects to show).
