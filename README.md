# FJR Landing Page

A static rebuild of the **First Job Interview Coaching – Perth** landing page,
originally published on Manus at
<https://jobcoachpert-h9rmrnjb.manus.space/>.

The original is a React single-page app (Tailwind + shadcn/ui) served from a
compiled bundle. This repo reimplements it as plain HTML and CSS with no build
step, no framework, and no JavaScript, so it can be hosted anywhere that serves
static files.

## Where the page came from

**Structure from the original** — section order, layout, spacing, type scale,
responsive breakpoints, card treatments, hover states and gradient dividers are
all derived from the original Manus markup.

**Copy has since moved on.** The hero and the "What We Coach" section were
rewritten and no longer match the original; the pricing cards, steps and footer
still carry the original wording.

**Palette and type from the brand guide.** Applying the guide moved three
things off the original design:

1. The header banner and footer are now **Deep Forest** (the guide assigns that
   colour to both).
2. Page backgrounds are **Warm Cream**, not white ("keep backgrounds warm").
3. The "Most Popular" badge label is charcoal rather than white — white on
   terracotta measures 2.7:1, which is unreadable. Charcoal gives 5.3:1.

## Logo

The masthead carries the FJR lockup — monogram flanked by terracotta rules,
wordmark beneath — in its reversed colourway (cream on Deep Forest).

It is built as **live text, not an image**. The supplied artwork was a raster
with a watermark, so it was rebuilt in HTML and CSS. That means it stays sharp
at any size and on any display, adds no image request, is selectable and
readable by screen readers, and the flanking rules space themselves off the
monogram rather than sitting at fixed coordinates — so nothing collides or
drifts if a font is slow to load or falls back.

To use the primary colourway on a light background, set `.logo` to
`color: rgb(var(--forest))`.

`images/favicon.svg` uses the same monogram.

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
"use sparingly" note. There the badge sweeps terracotta → champagne
(`#E5C185`) → terracotta so it reads as premium rather than as a status chip.
Champagne is a highlight stop for that gradient only, not a sixth brand
colour. The label stays charcoal, which clears 4.5:1 at every point along the
ramp (worst case 5.28:1 at the terracotta ends); white would drop to 1.71:1
over the champagne.

### Button colour

Buttons use `#538065`, one step darker than the brand sage — an 18% shift
toward Deep Forest. White label text on brand sage measures 3.87:1, under the
WCAG AA minimum of 4.5:1 for text at this size; the darker face clears it at
4.52:1. Sage itself is unchanged everywhere else on the page.

It is a single token at the top of `css/style.css`:

```css
--button-face: 83 128 101; /* #538065 */
```

Set it to `var(--primary)` to go back to the brand sage exactly.

## Typography

Per the brand guide's pairing rule — serif for headlines and section titles
only, sans-serif for body copy, buttons and UI text:

- **Lora** (400–700) — headings
- **Inter** (300–700) — body copy, buttons, prices, UI

Both load from Google Fonts.

## Booking

All three CTAs are anchors pointing at Calendly, opening in a new tab so the
landing page stays put:

| CTA | Event |
| --- | --- |
| Hero | `calendly.com/firstjobready/60-minute-mock-interview-coaching-session` |
| Practice Interview + Feedback | `calendly.com/firstjobready/20min` |
| Full Coaching Session | `calendly.com/firstjobready/60-minute-mock-interview-coaching-session` |

Both card durations match the copy on their cards.

Since every button reads "Book Now", each carries an `aria-label` naming its
package so they are distinguishable out of context.

In the pricing cards the buttons are pinned to the bottom edge with
`margin-top: auto`, so they sit on the same line across both cards however
long the descriptions run. The hero CTA takes `.button--inline`, which drops
the full-width rule since that is a card treatment.

To open bookings in the same tab instead, drop `target` and `rel` from the
anchors.

## Analytics

Microsoft Clarity (project `y2r8wl01qz`) is loaded from the end of `<head>` in
`index.html`. It records heatmaps and session replays. The snippet is async, so
it never blocks the page render, and it is the only JavaScript on the site.

Two things worth knowing:

- Clarity's terms put the duty of disclosure on the site owner. This page has
  no privacy notice yet, and its audience includes minors, so a short privacy
  statement is likely warranted before it sees real traffic.
- Session replay captures what visitors type and click. Clarity masks form
  fields by default, but the masking level is worth confirming in the Clarity
  dashboard under **Settings → Masking**.

To remove it, delete the `<script>` block at the end of `<head>`.

`privacy.html` describes what Clarity collects. It is deliberately **not**
tracked itself — the Clarity snippet is only in `index.html`. Add the same
`<script>` block to `privacy.html` if you would rather track both.

The notice is a starting draft written without access to primary sources, and
it carries an unfilled contact address. Both are flagged in the file with a
`TODO`. It should be reviewed by someone qualified before the site takes real
traffic.

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
index.html            Page markup
css/style.css         Brand tokens, reset, layout, components
privacy.html          Privacy notice
images/favicon.svg    FJR monogram favicon
```
