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

**Copy has since moved on.** The hero and "What We Coach" were rewritten, and
"About Your Coach" and the FAQ are new. Only the pricing cards, the steps and
the footer still carry original wording.

**Audience is early-career, not teens.** The word "teen" appears nowhere on the
landing page — the framing is anyone early in their career, including first
jobs, career changes and returns to work. Nerves stay in the copy as one reason
people struggle, alongside lack of interview practice.

Age and consent content lives **only** in `terms.html` (minimum age 14, parent
or guardian approval under 18), deliberately kept off the landing page.

> ⚠️ `privacy.html` still describes the service as being "for teenagers" in two
> places, which now contradicts the landing page and the terms. It was left
> alone on instruction. Worth reconciling.

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

Both CTAs are anchors pointing at Calendly, opening in a new tab so the
landing page stays put. The hero has no CTA of its own — booking happens from
the pricing cards only.

| CTA | Event |
| --- | --- |
| Practice Interview + Feedback | `calendly.com/firstjobready/20min` |
| Full Coaching Session | `calendly.com/firstjobready/60-minute-mock-interview-coaching-session` |

Both card durations match the copy on their cards.

The 20-minute session is on sale: `$39` struck through with `<s>`, `$29` beside
it. Because line-through is not announced by screen readers, the markup carries
`visually-hidden` "Was" and "now" labels, so it reads as *"Was $39, now $29"*.
No end date is set; `.package__sale-note` is styled and sits commented out in
the markup, so adding "Sale ends …" later is a text edit.

Since both buttons read "Book Now", each carries an `aria-label` naming its
package so they are distinguishable out of context.

In the pricing cards the buttons are pinned to the bottom edge with
`margin-top: auto`, so they sit on the same line across both cards however
long the descriptions run.

To open bookings in the same tab instead, drop `target` and `rel` from the
anchors.

## Analytics

Microsoft Clarity (project `y2r8wl01qz`) is loaded from the end of `<head>` in
`index.html`. It records heatmaps and session replays. The snippet is async, so
it never blocks the page render, and it is the only JavaScript on the site.

Two things worth knowing:

- Clarity's terms put the duty of disclosure on the site owner. `privacy.html`
  covers it, and is linked from the footer.
- Masking is set to **strict** in the Clarity dashboard, so page text is hidden
  in session replays. The privacy notice states this, so the two need to stay
  in step — if the masking level changes, update the notice.

To remove it, delete the `<script>` block at the end of `<head>`.

`privacy.html` describes what Clarity collects. It is deliberately **not**
tracked itself — the Clarity snippet is only in `index.html`. Add the same
`<script>` block to `privacy.html` if you would rather track both.

The notice is a starting draft written without access to primary sources, so
it should be reviewed by someone qualified before the site takes real traffic.

It carries **no contact details** by request. People who have booked can reach
us by replying to their Calendly confirmation, and the notice says so; visitors
who have not booked have no route to us except the OAIC. Adding an address
later means restoring a short "Contact us" section and pointing sections 4, 6
and 7 back at it.

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
index.html            Landing page
privacy.html          Privacy notice
terms.html            Terms & conditions
css/style.css         Brand tokens, reset, layout, components
images/favicon.svg    FJR monogram favicon
```

## Hero photograph

The hero is a photograph behind a dark scrim, with the copy over it.

`index.html` references **`images/hero-before-after.jpg`** (1828 × 861, the
split before/after interview shot). **The file is not in the repo yet** and has
to be uploaded. Save it as **JPEG** — as a PNG a photo this size runs several
megabytes.

### Why it does not break while the file is missing

`.hero` paints the scrim colour (`--hero-scrim`, `#16221B`) as its own
`background-color`, and the photo is a separate `<img>` layered behind the
scrim. If the image is missing, slow, or fails to decode, the hero falls back to
a solid dark band with the same cream type on it — a deliberate-looking hero
rather than a broken one.

### Legibility

Cream type over a photograph only works if the scrim guarantees it, so the scrim
is measured rather than eyeballed. Rendering the hero with the text hidden and
sampling the real composited pixels behind it gives:

| Width | Lightest background behind the copy | Cream on it |
| --- | --- | --- |
| 1280 px | `rgb(53, 62, 60)` | **10.24:1** |
| 360 px | `rgb(42, 53, 48)` | **11.82:1** |

Both clear WCAG AAA (7:1), let alone AA. Measured against a stand-in whose right
side ramps to pure white — brighter than the real photograph — so the real
numbers should be at least this good.

Two things hold that up, and both matter if the layout changes:

- **Below 768 px** the scrim is near-uniform and heavy (0.90 → 0.84). Narrow
  crops are unpredictable, so legibility cannot depend on which part of the
  photo lands behind the text.
- **At 768 px and up** the scrim turns directional — heaviest at the left where
  the copy sits, lifting to 0.32 at the right so the handshake stays visible —
  and the copy is capped at `34rem` to keep it inside the heavy end. Widening
  that cap would push text onto the bright side of the frame.

`object-position: 64% center` favours the right of the frame, so the anxious
half crops away first on narrow screens.

## About Your Coach illustration

One `.art` placeholder remains under "About Your Coach": dashed edge, tinted
ground, concept named in the middle, sized to reserve roughly the footprint the
real sketch will take.

Style direction: hand-drawn / sketchbook, loose linework, accent colour used
sparingly, faceless, age-neutral.

> The earlier two-chairs pencil sketch (`images/hero-interview.png`) is no
> longer referenced anywhere — the photograph took the hero slot. Nothing is
> broken by that, but the sketch currently has no home on the page.

## FAQ

Native `<details>` accordions — no JavaScript, keyboard-operable for free, and
the answers stay in the HTML so they remain findable while collapsed.

One flat list of five questions, no group headings. Ordered so the questions
about what the session actually is land before the logistics.

Two answers were removed from here on purpose: the refund question, which is
covered by `terms.html` §5, and the price question, which the pricing cards
already answer.
