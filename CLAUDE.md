# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Mányai Zoltán's personal bio/portfolio site. Fully static, zero-build, zero-dependency HTML+CSS+JS. No package.json, no bundler, no test suite — there is nothing to install or compile.

## Commands

Run locally:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`. Opening the files directly via `file://` also works. There is no lint/build/test command — verify changes by loading the page in a browser (or Playwright) and checking visually.

Deployment is GitHub Pages serving directly from the `main` branch root — a push to `main` is a push to production. Live URL: `https://menyuswin.github.io/manyai-zoltan/`.

Test mobile layouts with real device emulation (Playwright `devices['iPhone 13']` / `devices['iPhone SE']`), not just a narrow fixed viewport — a plain `{width: 375}` viewport ignores whether `<meta name="viewport">` is present. That meta tag was missing once and every mobile media query silently never fired on real phones while fixed-viewport tests passed.

## Head / SEO / link previews

Both pages carry, in their head: `<html lang="hu">`, the viewport meta, canonical, favicons, Open Graph + `twitter:card` tags, and a JSON-LD block (`ProfilePage` → `Person` with `@id …/#person` on the homepage; `WebPage` + `BreadcrumbList` pointing `about` at that same `@id` on `palyafutas/`). Keep the two pages consistent when touching any of these; a new page should get the same set.

- `og:image` must be an **absolute** URL (`https://menyuswin.github.io/manyai-zoltan/og-image.jpg`) — relative paths break previews in Signal/WhatsApp/LinkedIn. Messaging apps cache previews aggressively; after changing the image, change its filename (and the tags) to bust caches.
- `og-image.jpg` (1200×630) was composed from a background-removed portrait (rembg, `isnet-general-use` model) on a dark navy gradient with the site's gold accent, rendered from HTML with Playwright. The face sits near the horizontal center on purpose — WhatsApp and some clients center-crop to a square thumbnail. The site's Google Fonts are not reachable from the sandbox; for faithful renders load them locally from npm `@fontsource/{newsreader,public-sans,ibm-plex-mono}`.
- `sameAs` in the Person JSON-LD holds the LinkedIn profile URL (percent-encoded, tracking params stripped). Add other official profiles there, not in visible markup, if asked.
- There is intentionally **no `robots.txt`**: crawlers only read it at the domain root (`menyuswin.github.io/robots.txt`), and this is a project site under `/manyai-zoltan/`, so one here would be ignored. `sitemap.xml` is submitted directly in Google Search Console instead; bump its `<lastmod>` dates when page content changes meaningfully.

## Architecture

**Two HTML pages sharing one stylesheet**, not a single-page app:
- `index.html` — the main bio page (hero, Rólam, Szakterületek, Média-megjelenések, Produktumok, Tanulmányok, Kapcsolat sections, all on one page via anchor links).
- `palyafutas/index.html` — a **standalone page**, not a modal/tab. It exists as its own file (served at `/palyafutas/`) specifically so it can carry its own `<link rel="canonical">`, `<title>`, and `meta description` distinct from the homepage. An earlier version used a JS-driven modal keyed off a `#palyafutas` URL hash; that was replaced because a hash fragment never reaches the server and Google treats it as the same document as the hash-less URL — it can't be independently canonical. If asked to make some other section "shareable/indexable in its own right," this is the precedent: it needs a real file/path, not a hash or client-side route.
- `style.css` — shared by both pages. Edit once, both pages pick it up. There's no build step to bundle/purge it, so it just grows; keep related rules grouped under the existing `/* ---- section ---- */` comments.

**Keeping two pages in sync is manual.** The masthead, topbar (including nav), and footer markup are duplicated between `index.html` and `palyafutas/index.html`. There's no include/template mechanism — if you change the topbar in one, change it in the other too. `palyafutas/index.html` references shared assets one level up (`../style.css`, `../header.jpg`) and links back to homepage sections as `../#produktumok` etc.

**Topbar nav renders as buttons, not text links** (`style.css`, `.topbar-nav a`): solid accent-colored fill, same visual weight as the `.topbar-cta` "Kapcsolat" button. The current page is marked with `aria-current="page"` on its own nav link, which flips it to an inverse/outline treatment via `.topbar-nav a[aria-current="page"]` — this is the only way "you are here" is indicated, so don't reintroduce a second "Kapcsolat" entry or drop `aria-current` when touching nav markup.

**Theming**: CSS custom properties on `:root`, redefined under `@media (prefers-color-scheme: dark)` and again under `:root[data-theme="dark"]` for an explicit override (nothing currently sets `data-theme`, but the CSS supports it). Any new color must be added to both the light block and both dark blocks.

**Press widget** (`index.html` only, not on the Pályafutás subpage): a self-contained script that fetches 6 Hungarian news RSS feeds client-side through `rss2json.com`'s free proxy (feeds' own CORS blocks direct fetches), caches the result in `localStorage` for 30 minutes, and renders into a slide-in panel. It's independent of the rest of the page's JS.

**Produktumok section** links out to sibling projects that live in their own repos/Pages sites — this repo does not contain their code:
- `angol-keresztrejtveny` — Angol szókincs keresztrejtvény
- `Menyusweather` — Menyusweather
- `nevnapnaptar` — Kalendárium (renamed from "Névnapnaptár"; keep the card text and this repo's README in sync if that project's scope changes again)

Card copy in the Produktumok section and the README's product list should describe what a linked project *currently* does — they've drifted out of sync with the linked repos before (a rename there didn't get reflected here immediately) and needed a follow-up fix.
