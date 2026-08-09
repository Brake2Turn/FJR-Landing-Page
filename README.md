# FJR Landing Page

A static rebuild of the **First Job Interview Coaching – Perth** landing page,
originally published on Manus at
<https://jobcoachpert-h9rmrnjb.manus.space/>.

The original is a React single-page app served from a compiled bundle. This
repo reimplements it as plain HTML and CSS with no build step, so it can be
hosted anywhere that serves static files.

## Status

⚠️ **Scaffold only — page content is not in place yet.**

The `<head>` in `index.html` (title, canonical URL, Open Graph and Twitter
metadata, font loading) is recovered verbatim from the original. The `<body>`
is a placeholder.

The remaining work is to fill in the body from the original page's rendered
DOM. Because the source is a SPA, View Source returns only `<div id="root">`
— the copy has to come from DevTools → Elements → right-click `<div id="root">`
→ Copy → Copy outerHTML.

## Typography

Carried over from the original:

- **Lora** (400–700) — display and headings
- **Inter** (400–700) — body text

Both are loaded from Google Fonts.

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
index.html      Page markup (head recovered from original; body pending)
css/style.css   Design tokens, reset, base typography
```
