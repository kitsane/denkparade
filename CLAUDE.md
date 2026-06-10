# Denkparade GmbH – Website

Static website for Denkparade GmbH (Claudia Staub, Zürich) – consulting for
strategy and sustainability projects. German-language, four pages.

## Hard constraints

- **Minimal JavaScript.** Everything works with plain HTML/CSS. The mobile menu
  is a hidden-checkbox + label pattern, the contact form posts via
  `mailto:` (`enctype="text/plain"`), the footer year is hardcoded. Two allowed
  `<script>` tags in `index.html`: the inert JSON-LD block, and a 3-line inline
  handler that unchecks the menu checkbox when a nav anchor is tapped (anchor
  navigation doesn't reload the page, so CSS alone can't close the menu).
  Don't add more JS.
- **No build step.** Files are deployed exactly as they are in the repo.
- **One page.** All sections live in `index.html`; the nav scrolls to anchors
  (`#ueber-mich`, `#angebot`, `#kontakt`) via CSS `scroll-behavior: smooth`
  (disabled under `prefers-reduced-motion`).
- All asset/link paths are **relative**, because GitHub Pages serves the site
  under the `/denkparade/` subpath. Keep them relative.

## Structure

| File | Purpose |
|---|---|
| `index.html` | Whole site: hero, Über mich, Angebot (three cards), Kontakt (info + mailto form) |
| `styles.css` | Single stylesheet |
| `assets/claudia-portrait.jpg` | Web copy of the portrait |
| `CNAME` | Custom domain for GitHub Pages (`www.denkparade.ch`) – do not delete |

## Layout invariants

- Sticky footer: `body` is a flex column with `min-height: 100svh`.
- The hero has **no** generic section padding (`padding: 0`) and
  `min-height: calc(100svh - 4rem)` so it fills exactly the first viewport
  below the 4rem sticky header; its `.container` centers via
  `margin-block: auto`.
- `scroll-padding-top: 5rem` on `html` keeps anchor targets clear of the
  sticky header – keep it in sync if the header height changes.
- Heading hierarchy: one `h1` (hero), sections are `h2`, offer cards `h3`.
- Breakpoints: offer grid/about collapse below 56rem, burger menu below 40rem.

## Accessibility (preserve all of this)

The site targets WCAG 2.1 AA. In place and verified – don't regress:

- **Color contrast**: every text/background pair is ≥ 4.5:1 (lowest: muted
  `#6b7280` on `#f8f9fb` at 4.59:1; body text on white is 7.56:1). When adding
  colors, check contrast before using them for text.
- **Keyboard**: skip link as first focusable element on every page; global
  `:focus-visible` outline; the CSS-only burger menu stays keyboard-operable
  because the hidden checkbox is focusable (Tab + Space) and its focus ring is
  drawn on the visible label via `.nav-checkbox:focus-visible ~ .nav-toggle`.
  Never hide the checkbox with `display: none` – that removes it from the tab
  order.
- **Semantics**: one `h1`, `<nav aria-label>`, landmarks
  (`header`/`main`/`footer`), labeled form fields with `autocomplete`,
  `required` for native validation.
- **Screen readers**: decorative SVGs and the badge numbers are
  `aria-hidden="true"`; the portrait has descriptive German alt text.
- **Motion**: `prefers-reduced-motion: reduce` disables smooth scrolling and
  transitions.
- Touch targets (burger, inputs, buttons) are ≥ 44px.

Language is German – keep `lang="de"` and write alt texts/labels in German.

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
