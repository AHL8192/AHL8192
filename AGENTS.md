# AGENTS.md — AHL8192 profile README

This repo is the GitHub **profile README** for `AHL8192` (the repo must stay named
`AHL8192/AHL8192`, public, with `README.md` at the root). Everything here is
hand-built: no GitHub Actions, no build step, no external theme.

Read this before changing the look.

---

## 1. Files

| Path | What it is |
|---|---|
| `README.md` | The whole page: layout, text, and every widget URL |
| `assets/hero-dark.svg` | 1280×360 hero, dark mode |
| `assets/hero-light.svg` | 1280×360 hero, light mode |
| `assets/rule-dark.svg` | 1280×30 glass divider, dark mode |
| `assets/rule-light.svg` | 1280×30 glass divider, light mode |

The hero and rules are inline SVG with SMIL animation (the slow light sweep).
They are referenced with **relative** paths (`assets/...`), never raw URLs, so
edits go live as soon as they are pushed.

---

## 2. Design system — "Aero Glass"

Deep navy glass, one cyan accent, a single warm highlight, lots of air.
Frutiger-Aero / Windows 7 revival.

### Palette

| Token | Dark | Light | Used for |
|---|---|---|---|
| Page / card bg | `#0d1117` | `#f5fbff` | cards, widget backgrounds |
| Card border | `#1F3A52` | `#D6E9F5` | card outlines |
| Title | `#7EE0FF` | `#12526F` | card titles, headings |
| Body | `#CFE9F5` | `#334E5C` | card text |
| Accent | `#4CC2FF` | `#1F8FC4` | icons, typing line, links |
| Muted | `#8FB3C7` | `#6B8A9A` | dates, secondary text |
| Warm | `#FFB86B` | `#FF9A4D` | streak flame only |

Hero backgrounds live in the SVGs:

- Dark: `#071322 → #0B1B2B → #0E2A40`
- Light: `#F5FBFF → #DFEFFB → #C8E6F7`

Rule: **one accent, one warm pop, nothing else.** If a new element needs a
colour, reuse a token above.

### Type

- Hero: `'Segoe UI', Inter, 'Helvetica Neue', Arial, sans-serif`, 86px/700 name.
- Typing line: Fira Code 21px (via readme-typing-svg).
- Body: GitHub's own type stack — never try to set fonts in Markdown.
- Small captions use `<sub>` (0.75em, muted).

---

## 3. Page structure (top to bottom)

1. **Hero** — `<picture>` → `assets/hero-dark.svg` / `hero-light.svg`, `width="100%"`.
2. **Typing line** — readme-typing-svg, cycles the four roles.
3. **Intro** — one italic sentence, centred.
4. **Rule**
5. **About panel** — 3-column `<table>`: 🛠 Building · ✍️ Writing · 🎬 Filming.
   The table borders are intentional here (spec-sheet look).
6. **Stack** — skillicons.dev, 10 icons, `perline=10`.
7. **Rule**
8. **Featured work** — 4 pinned repo cards, 2 per row, `width="49%"`.
9. **Rule**
10. **The numbers** — stats `48%` + top-langs `43%` on one line, streak `60%` below.
11. **Rule**
12. **Elsewhere** — YouTube / Medium / Telegram / GitHub shields.
13. **Footer** — visitor counter + signature.

Keep the rule between major blocks. Don't add more than one new section without
removing another; the page is tuned to ~2.5 screens.

---

## 4. The one pattern to copy: theme-aware images

GitHub supports `prefers-color-scheme` in `<picture>`. **Source order matters**
(dark first, light second) and the `<img>` fallback must be the dark URL.

```html
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)"  srcset="DARK_URL">
    <source media="(prefers-color-scheme: light)" srcset="LIGHT_URL">
    <img src="DARK_URL" alt="..." width="48%">
  </picture>
</p>
```

Every image on the page has both variants. If you add one, add both.

---

## 5. How to change things

### Text

All copy is in `README.md`. Keep the voice short and dry. Do not invent personal
facts — the only confirmed ones are the four roles and the repos.

The Writing/Filming panel lines are placeholders marked `<!-- EDIT ME -->`.
Replace them when the user supplies real copy, then delete the comment.

### Hero

Edit `assets/hero-*.svg`. Keep `viewBox="0 0 1280 360"` and keep text inside
`x=84…620` — the orb owns the right side. Keep the `<animate>` sweep and the
`<title>` for accessibility. Update both files in parallel; the light file is a
colour-swapped copy, not a separate design.

### Palette

Two places:

1. The four SVGs (hero gradients, orb, text colours).
2. Hex params in the widget URLs in `README.md`. Search/replace:

| Find | Replace (example) |
|---|---|
| `0d1117` | new dark card bg |
| `1F3A52` | new dark border |
| `7EE0FF` | new dark title |
| `CFE9F5` | new dark body |
| `4CC2FF` | new dark accent |
| `f5fbff` | new light card bg |
| `D6E9F5` | new light border |
| `12526F` | new light title |
| `334E5C` | new light body |
| `1F8FC4` | new light accent |

The typing line colour (`7EE0FF` / `1F8FC4`) and the streak `fire` (`FFB86B` /
`FF9A4D`) are in the URLs too.

### Featured repos

Each card is a pin URL. Change the `repo=` value in **all three** places per card
(dark `<source>`, light `<source>`, fallback `<img>`). Keep
`description_lines_count=2` so all cards stay the same height.

### Stats row widths

The two cards are deliberately different widths so their heights match:

- stats card aspect ≈ 467:195 (2.39)
- top-langs compact 4 aspect ≈ 300:140 (2.14)

`48%` + `43%` makes both ~190px tall at the profile width. If you change
`langs_count`, recompute: `width% ≈ (48% × 2.39) / new_aspect`. Otherwise the
row goes ragged (and inline images align on the baseline, so it shows).

### Add a social button

```html
<a href="URL"><img src="https://img.shields.io/badge/NAME-0B1B2B?style=for-the-badge&logo=SLUG&logoColor=ACCENT" alt="NAME"></a>
```

Use the same dark chip for both themes. `logo` is a Simple Icons slug.

---

## 6. Widget reference

| Widget | Endpoint | Key params |
|---|---|---|
| Typing | `readme-typing-svg.demolab.com` | `font=Fira+Code`, `size=21`, `pause=1300`, `color`, `width=720`, `lines` separated by `;` |
| Icons | `skillicons.dev/icons` | `i=...`, `theme=dark`, `perline=10` |
| Stats | `github-readme-stats.vercel.app/api` | `show_icons`, `include_all_commits`, `rank_icon=github`, `bg_color`, `title_color`, `text_color`, `icon_color`, `border_color`, `hide_border=false`, `border_radius=12` |
| Languages | `.../api/top-langs` | `layout=compact`, `langs_count=4`, same colours |
| Repo pin | `.../api/pin` | `repo=...`, `description_lines_count=2`, same colours |
| Streak | `streak-stats.demolab.com` | `border`, `background`, `stroke`, `ring`, `fire`, `currStreakLabel`, `sideLabels`, `dates`, `currStreakNum`, `sideNums`, `border_radius=12` |
| Visitors | `komarev.com/ghpvc` | `username`, `label=VISITORS`, `color=4CC2FF`, `style=flat-square` |
| Socials | `img.shields.io/badge` | `style=for-the-badge`, `logo`, `logoColor` |

All endpoints were verified returning `200 image/svg+xml` at build time. They are
third-party services: if one starts failing (402/500), replace it rather than
leaving a broken image.

---

## 7. Preview locally (do this before pushing)

GitHub's own Markdown renderer + headless Chromium gives an accurate preview.

```bash
cd /home/ahl8192/Documents/dev/github-profile
mkdir -p /tmp/opencode/preview && cd /tmp/opencode/preview
# once: npm init -y && npm i playwright@1.64.1 && npx playwright install chromium

# 1. GitHub's renderer -> HTML fragment
jq -Rs '{text: ., mode: "gfm"}' /home/ahl8192/Documents/dev/github-profile/README.md \
  | gh api -X POST /markdown --input - > body.html

# 2. wrap it and screenshot (dark + light)
```

Minimal wrapper + shot script (`render.js`):

```js
const { chromium } = require('playwright');
const fs = require('fs');
const dir = '/tmp/opencode/preview';
const repo = '/home/ahl8192/Documents/dev/github-profile';
const body = fs.readFileSync(`${dir}/body.html`, 'utf8');
const page = (theme, bg) => `<!doctype html><html><head><meta charset="utf-8">
<base href="file://${repo}/">
<link rel="stylesheet" href="file://${dir}/gh-${theme}.css">
<style>html,body{margin:0;background:${bg}}
.markdown-body{box-sizing:border-box;max-width:1012px;margin:0 auto;padding:32px}</style>
</head><body><article class="markdown-body">${body}</article></body></html>`;
// fetch github-markdown-css once:
// curl -sLo gh-dark.css  https://cdn.jsdelivr.net/npm/github-markdown-css@5/github-markdown-dark.css
// curl -sLo gh-light.css https://cdn.jsdelivr.net/npm/github-markdown-css@5/github-markdown-light.css
fs.writeFileSync(`${dir}/preview-dark.html`,  page('dark',  '#0d1117'));
fs.writeFileSync(`${dir}/preview-light.html`, page('light', '#ffffff'));

(async () => {
  const browser = await chromium.launch();
  for (const theme of ['dark', 'light']) {
    const ctx = await browser.newContext({
      viewport: { width: 1280, height: 2000 }, // tall so offscreen cards animate in
      colorScheme: theme,
    });
    const p = await ctx.newPage();
    await p.goto(`file://${dir}/preview-${theme}.html`, { waitUntil: 'networkidle' });
    await p.waitForFunction(() => [...document.images].every(i => i.complete && i.naturalWidth > 0)).catch(() => {});
    await p.waitForTimeout(9000);
    await p.screenshot({ path: `${dir}/shot-${theme}.png`, fullPage: true });
    await ctx.close();
  }
  await browser.close();
})();
```

### Preview gotchas (learned the hard way)

- The `<base href>` makes relative `assets/` work, but it also rewrites the CSS
  `<link>`. Use an **absolute** `file://` path for `gh-*.css`, or all text
  renders black.
- Stats/streak/pin SVGs fade in with CSS animations. Screenshot only after a
  **tall viewport** (2000px) and ~9s, otherwise cards look half-empty.
- The typing SVG is blank at random moments (it erases between lines). For a
  clean screenshot, render a temp copy with `pause=1300` → `pause=100000`.
- GitHub proxies external images through camo, so their `src` in the live DOM is
  a `camo.githubusercontent.com` URL — don't search the DOM for the service name.
- Repo-local SVGs are served directly and update immediately; external widgets
  are cached and may lag.

---

## 8. Ship it

```bash
git add -A
git commit -m "Describe the visual change"
git push origin main
```

Then confirm the live page at <https://github.com/AHL8192>. The profile README
renders from `main` with no deploy step.

---

## 9. Guardrails

- **Never use `style="..."`** — GitHub strips it. Layout is `<p align>`,
  `<table>`, `<picture>`, `width`/`height` attributes, and `<sub>`.
- **Never use Markdown/HTML tables for card grids** — GitHub's CSS draws borders
  on every cell. Use inline images in a centred `<p>`. Tables are only for the
  three-column about panel.
- Keep the `<picture>` source order (dark, light) and the dark fallback `<img>`.
- Keep repo assets relative; keep `alt` text on every meaningful image.
- Inline images align on the baseline — match heights via width percentages.
- No GitHub Actions unless the user asks. "Standard" mode is deliberate.
- Don't add a contribution heatmap: the free activity-graph services are
  paywalled (402) and the alternatives need Actions or force a light background.
- Don't invent bio details, links, or quotes.

---

## 10. Known open items

- **YouTube link is dead.** `https://www.youtube.com/@AHL8192` returns 404. The
  button still points there. Replace it when the user provides the current
  channel URL.
- **Writing / Filming copy** are placeholders (`<!-- EDIT ME -->`).
- **Repo website field** still points at the repo itself
  (`https://github.com/AHL8192`); replace with a real destination if given.
- Stats/langs percentages include forked repos (Shell is inflated by forks).
  If that matters, add `&exclude_repo=...` to the top-langs URL.
