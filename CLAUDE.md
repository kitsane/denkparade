# Denkparade GmbH – Website

Static website for Denkparade GmbH (Claudia Staub, Zürich) – consulting for
strategy and sustainability projects. German-language, four pages.

## Hard constraints

- **No JavaScript.** Everything works with plain HTML/CSS. The mobile menu is a
  hidden-checkbox + label pattern, the contact form posts via
  `mailto:` (`enctype="text/plain"`), the footer year is hardcoded. The only
  `<script>` tag in the project is the inert JSON-LD block in `index.html`.
- **No build step.** Files are deployed exactly as they are in the repo.
- **Separate pages, not a SPA.** Each nav item is its own HTML file; do not
  convert to JS-driven show/hide sections.
- All asset/link paths are **relative**, because GitHub Pages serves the site
  under the `/denkparade/` subpath. Keep them relative.

## Structure

| File | Purpose |
|---|---|
| `index.html` | Hero ("Beratung. Projektleitung. Strategie.") – must fit the viewport without scrolling |
| `ueber-mich.html` | About page with portrait |
| `angebot.html` | Three offer cards (Beratung / Projektleitung / Strategieentwicklung) |
| `kontakt.html` | Contact info + mailto form |
| `styles.css` | Single stylesheet for all pages |
| `assets/claudia-portrait.jpg` | Web copy of the portrait |

The header/footer markup is duplicated across all four pages (no templating) –
when changing it, change it in **all four files**.

## Layout invariants

- Sticky footer: `body` is a flex column with `min-height: 100svh`; `main` and
  its single `section` stretch. The footer must always sit at the viewport
  bottom on short pages.
- The hero section has **no** generic section padding (`padding: 0`) so the
  index page never scrolls on desktop viewports; its `.container` centers via
  `margin-block: auto`.
- Breakpoints: offer grid/about collapse below 56rem, burger menu below 40rem.

## Design source

The layout follows the mockups embedded in `Text_Webseite.docx` (git-ignored,
kept locally next to the repo together with the original portrait photo).
Fonts: Space Grotesk (headings) + Inter (body) via Google Fonts. Accent colors
for the offer-card badges: lilac `#d8d2f0`, yellow-green `#e0e1a9`,
pink `#f2c7d5`; ink color `#1f2937`.

## Deployment

- GitHub Pages serves the **`gh-pages`** branch of
  `github.com:kitsane/denkparade` → https://kitsane.github.io/denkparade/
- Deploy after changes on `main`: `git push origin main:gh-pages`
- The custom domain `denkparade.ch` is planned. Canonical URLs, `sitemap.xml`,
  and `robots.txt` already point to `https://www.denkparade.ch/` – update all
  three together if the final domain differs.

## Local preview

```
python3 -m http.server 8741
```

then open http://localhost:8741/ – no build step needed.
