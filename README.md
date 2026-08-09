# FJR Landing Page

A static rebuild of the **First Job Interview Coaching – Perth** landing page,
originally published on Manus at
<https://jobcoachpert-h9rmrnjb.manus.space/>.

The original is a React single-page app (Tailwind + shadcn/ui) served from a
compiled bundle. This repo reimplements it as plain HTML and CSS with no build
step, no framework, and no JavaScript, so it can be hosted anywhere that serves
static files.

## What's faithful, and what isn't

**From the original** — all copy is verbatim, and the section order, layout,
spacing, type scale, responsive breakpoints, card treatments, hover states and
gradient dividers are derived from the original markup.

**From the brand guide** — the palette and type pairing. Applying the guide
moved three things off the original design:

1. The header banner and footer are now **Deep Forest** (the guide assigns that
   colour to both).
2. Page backgrounds are **Warm Cream**, not white ("keep backgrounds warm").
3. The "Most Popular" badge label is charcoal rather than white — white on
   terracotta measures 2.7:1, which is unreadable. Charcoal gives 5.3:1.

**Still outstanding** — the banner artwork. The original is hosted on Manus
storage (`fjr_banner_3e3be417.png`). `images/fjr-banner.svg` is a brand-coloured
stand-in wordmark. Drop the real file into `images/` and update the one `src` in
`index.html`.

## Palette

Straight from the brand guide, defined once at the top of `css/style.css`:

| Role | Colour | |
| --- | --- | --- |
| Primary | Sage Green | `#5B8C6E` |
| Secondary | Deep Forest | `#2F4A3B` |
| Accent | Warm Terracotta | `#D98B5F` |
| Neutral | Warm Cream | `#FAF6F0` |
| Neutral | Charcoal Text | `#2B2B28` |

Terracotta appears exactly once, on the "Most Popular" badge, per the guide's
"use sparingly" note.

### One accessibility caveat

White on Sage Green measures **3.87:1** — under the WCAG AA minimum of 4.5:1
for text at button size. That affects the two "Book Now" buttons. Every other
pairing on the page passes, several comfortably.

The brand sage is used as specified rather than silently altered. If you'd
rather the buttons meet AA, uncomment one line in `css/style.css`:

```css
/* --button-face: 83 128 101; */
```

That darkens the sage by 18% toward Deep Forest (`#538065`, 4.52:1) for button
faces only — the brand sage stays exactly as specified everywhere else.

## Typography

Per the brand guide's pairing rule — serif for headlines and section titles
only, sans-serif for body copy, buttons and UI text:

- **Lora** (400–700) — headings
- **Inter** (300–700) — body copy, buttons, prices, UI

Both load from Google Fonts.

## Known quirk kept from the original

In the pricing cards the "Book Now" buttons sit directly after the description
rather than being pinned to the card's bottom edge, so they don't line up
across the two cards when the descriptions differ in length. That's how the
original renders. To align them, add `margin-top: auto` to `.button`.

The buttons are also inert — the original had no booking link wired up. Both
are marked with a `TODO` in `index.html`.

## Local preview

No build tools required. From the project root:

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Publishing to GitHub Pages

1. **Settings → Pages**
2. Under "Build and deployment", set the source branch to `main` and the folder
   to `/ (root)`
3. Wait a minute for the first publish, then open the `https://….github.io/…`
   URL it gives you

## Project structure

```
index.html              Page markup
css/style.css           Design tokens, reset, layout, components
images/fjr-banner.svg   Placeholder banner — replace with the real artwork
```
