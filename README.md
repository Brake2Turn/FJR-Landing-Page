# FJR Landing Page

A static rebuild of the **First Job Interview Coaching – Perth** landing page,
originally published on Manus at
<https://jobcoachpert-h9rmrnjb.manus.space/>.

The original is a React single-page app (Tailwind + shadcn/ui) served from a
compiled bundle. This repo reimplements it as plain HTML and CSS with no build
step, no framework, and no JavaScript, so it can be hosted anywhere that serves
static files.

## What's faithful, and what isn't

**Faithful** — all copy is verbatim from the original, and the section order,
layout, spacing, type scale, responsive breakpoints, card treatments, hover
states and gradient dividers are all derived from the original markup.

**Reconstructed** — two things could not be recovered:

1. **Colours.** The original's compiled stylesheet wasn't retrievable, so the
   shadcn token *roles* (`primary`, `secondary`, `accent`, `muted-foreground`,
   …) are preserved but the hex values are a choice. All six live at the top of
   `css/style.css` — edit those and the whole page retints.
2. **Banner artwork.** The original banner is hosted on Manus storage
   (`fjr_banner_3e3be417.png`). `images/fjr-banner.svg` is a stand-in. Drop the
   real file into `images/` and update the one `src` in `index.html`.

## Typography

Carried over from the original:

- **Lora** (400–700) — headings and prices
- **Inter** (300–700) — body text

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
