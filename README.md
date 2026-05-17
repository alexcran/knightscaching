# Knightscaching

Static site for the Knightscaching geocaching crew, built with [Astro](https://astro.build).

---

## Quick start

```bash
npm install       # install dependencies (first time only)
npm run dev       # start local dev server at http://localhost:4321
npm run build     # build the static site into dist/
npm run preview   # preview the built site locally
```

---

## File structure

```
knightscaching/
├── public/                          # Files served verbatim at the root URL
│   ├── favicon.svg
│   ├── topo.svg                     # Background topo pattern (used by CSS)
│   └── assets/
│       ├── caches/
│       │   └── GC12345/             # One folder per GC code
│       │       └── (your files)     # Accessible at /assets/caches/GC12345/…
│       └── images/
│           └── (profile photos,     # Accessible at /assets/images/…
│               landscapes, etc.)
│
├── src/
│   ├── components/
│   │   ├── Header.astro             # Site-wide header + mobile nav
│   │   ├── Footer.astro             # Site-wide footer
│   │   └── CacherCard.astro        # Card component used on the homepage
│   │
│   ├── layouts/
│   │   └── BaseLayout.astro        # Wraps every page (head, fonts, header, footer)
│   │
│   ├── pages/
│   │   ├── index.astro             # Homepage  →  /
│   │   ├── alexcran421.astro       # Cacher page  →  /alexcran421
│   │   ├── bosoxfansinnewjersey.astro
│   │   ├── jazzhorse89.astro
│   │   └── ATTweedleDum.astro
│   │
│   └── styles/
│       └── global.css              # Full design system (colors, typography, layout)
│
├── astro.config.mjs                # Astro config (static output, site URL)
├── package.json
└── README.md                       # This file
```

---

## How to edit content

### Change the tagline or homepage intro

Open `src/pages/index.astro`. The hero tagline and crew intro text are plain strings — edit them directly.

### Edit a cacher's bio

Open `src/pages/<handle>.astro`. Find the `<div class="profile-bio-text">` block and replace the placeholder paragraphs with real text.

### Add a profile photo

1. Drop the photo into `public/assets/images/<handle>.jpg` (or `.png`).
2. In the cacher's `.astro` page, replace this block:

```html
<div class="profile-photo" role="img" aria-label="Profile photo placeholder">
  …svg placeholder…
  <span class="profile-photo-label">Profile Photo</span>
</div>
```

with:

```html
<img
  src={`/assets/images/${handle}.jpg`}
  alt={`${handle} profile photo`}
  class="profile-photo-img"
/>
```

Then add this CSS to `src/styles/global.css`:

```css
.profile-photo-img {
  width: 100%;
  aspect-ratio: 1;
  object-fit: cover;
}
```

### Paste a stats embed

In each cacher's `.astro` page, find the comment:

```html
<!-- PASTE STATS EMBED HERE -->
```

Replace the `<div class="stats-embed-area">…</div>` that follows it with your iframe or widget HTML.

### Add a cache file directory

Create a folder under `public/assets/caches/` named after the GC code:

```
public/assets/caches/GC99ABC/hint.jpg
```

This file becomes accessible at `https://knightscaching.com/assets/caches/GC99ABC/hint.jpg`.
You can then link to it from your geocaching.com listing page.

---

## Design tokens

Colors, fonts, and spacing are defined as CSS custom properties at the top of
`src/styles/global.css`. To change the color scheme, edit the `:root { … }` block there.

| Token | Value | Use |
|---|---|---|
| `--navy-900` | `#0D1B2A` | Primary background |
| `--green-900` | `#1A2E23` | Hero gradient accent |
| `--ochre-400` | `#C4943A` | Gold accent / labels |
| `--stone-100` | `#F5F2ED` | Light text on dark bg |
| `--font-display` | Space Grotesk | Headings |
| `--font-body` | Inter | Body text |
| `--font-mono` | IBM Plex Mono | Labels, coordinates, code |

---

## Deploying

Run `npm run build` — the static output lands in `dist/`. Upload the contents of
`dist/` to any static host (Netlify, Vercel, GitHub Pages, Cloudflare Pages, etc.).

For Netlify: connect the repo, set build command to `npm run build`, publish directory to `dist`.
