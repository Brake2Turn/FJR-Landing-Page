# FJR Landing Page

A static rebuild of the **First Job Interview Coaching – Perth** landing page,
originally published on Manus at
<https://jobcoachpert-h9rmrnjb.manus.space/>.

The original is a React single-page app (Tailwind + shadcn/ui) served from a
compiled bundle. This repo reimplements it as plain HTML and CSS with no build
step, no framework, and no JavaScript, so it can be hosted anywhere that serves
static files.

## Where the page came from

**Structure from the original** — layout, spacing, type scale, responsive
breakpoints, card treatments, hover states and gradient dividers are all derived
from the original Manus markup.

Section order has since diverged. It now runs: hero, What We Coach, About Your
Coach, Coaching Packages, What Happens After You Book, FAQ. Tinted and plain
backgrounds alternate down the page, so adding or reordering a section means
checking that `.section--tinted` still lands on every other one.

"What We Coach" is a row of three equal cards (`.topics` / `.topic`), not the
numbered list it started as — the three items are parallel topics rather than
steps in a sequence, so nothing is numbered. Grid gives them a shared row height
whatever length the copy runs to.

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

| File | Size | Dimensions |
| --- | --- | --- |
| `images/hero-before-after.jpg` | 103 KB | 1823 × 863 |
| `images/hero-before-after-960.jpg` | 40 KB | 960 × 454 |

Served through `srcset` with `sizes="100vw"`, so phones fetch the 960 px file
and desktops the full one.

### Provenance

The photo arrived in the repo as `hero-before-after.jpg.png` — a 1.46 MB **PNG**
with a doubled extension, so the page could not find it. It was re-encoded here
to progressive JPEG at quality 82 (4:2:2 chroma), which is a **94% reduction**
with no visible loss at this size, especially under the scrim. The misnamed
original was removed.

If the photo is ever replaced, re-encode rather than dropping a PNG in: a
full-width photo as PNG costs well over a megabyte on the first paint.

### Why it does not break if the image goes missing

`.hero` paints the scrim colour (`--hero-scrim`, `#16221B`) as its own
`background-color`, with the photo as a separate `<img>` layered behind the
scrim. A missing, slow or undecodable image leaves a solid dark band carrying
the same cream type — a deliberate-looking hero rather than a broken one.

### Legibility

Cream on a photograph only works if the scrim guarantees it, so the scrim is
measured, not eyeballed: the hero is rendered with its text hidden and the real
composited pixels behind each line are sampled for the lightest one.

| Width | Lightest background behind the copy | Cream on it |
| --- | --- | --- |
| 1280 px | `rgb(71, 79, 72)` | **7.87:1** |
| 360 px | `rgb(64, 71, 65)` | **8.88:1** |

Both clear WCAG AAA (7:1). Desktop is the tighter of the two, because the bright
window in the upper right of the frame reaches the right edge of the text column.

Two mechanisms hold that up, and both matter if the layout changes:

- **Below 768 px** the scrim is near-uniform (0.85 → 0.77). Narrow crops are
  unpredictable, so legibility cannot depend on which part of the photo lands
  behind the text. It was originally heavier still, and was lightened once
  measurement showed the headroom — at 0.90 the photograph barely read on a
  phone.
- **At 768 px and up** the scrim turns directional — 0.94 at the left where the
  copy sits, lifting to 0.32 at the right so the handshake stays visible — and
  the copy is capped at `34rem` to keep it inside the heavy end. Widening that
  cap, or lightening the left stop, would push the desktop figure below AAA.

`object-position: 64% center` favours the right of the frame. At desktop widths
the full width of the photo fits, so it only affects narrow screens, where it
keeps the handshake rather than the anxious half.

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
