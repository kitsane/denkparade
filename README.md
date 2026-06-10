# Denkparade GmbH – Website

One-page website for [Denkparade GmbH](https://www.denkparade.ch/) – Beratung,
Projektleitung und Strategieentwicklung mit Fokus auf Nachhaltigkeit
(Claudia Staub, Zürich).

Plain HTML and CSS, no build step, (almost) no JavaScript.

## Tech notes

- **Single page** (`index.html`) with anchor navigation and smooth scrolling;
  sections: Hero, Über mich, Angebot, Kontakt.
- **No frameworks, no bundler** – the repo is deployed as-is.
- **JS-free by design**: the mobile menu is a CSS checkbox pattern and the
  contact form opens the visitor's mail client via `mailto:`. The only script
  is a small progressive enhancement (scrollspy nav highlight + closing the
  mobile menu after an anchor tap).
- Accessibility: WCAG AA contrast, skip link, keyboard-operable menu,
  `prefers-reduced-motion` support.
- SEO: meta/OG tags, JSON-LD structured data, `sitemap.xml`, `robots.txt`.

## Development

No tooling required:

```sh
python3 -m http.server 8741
# open http://localhost:8741/
```

## Deployment

Hosted on GitHub Pages from the `gh-pages` branch, domain
`www.denkparade.ch` (see `CNAME`). Deploy after changes on `main`:

```sh
git push origin main main:gh-pages
```

## Fonts & license notes

[Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk) (headings)
and [Inter](https://fonts.google.com/specimen/Inter) (body) are loaded via
Google Fonts; both are licensed under the SIL Open Font License. The favicon
is the Space Grotesk Bold "D" embedded as a static SVG path.

Website content and photos © Denkparade GmbH. All rights reserved.
