# AI Handoff

_Last updated: 2026-11-05 (America/New_York)_

## Current state
- Live: https://arcade.brewdadlabs.com (custom domain on Cloudflare Pages project `brewdadlabs-arcade`).
- Pages URLs: https://brewdadlabs-arcade.pages.dev (production), https://preview.brewdadlabs-arcade.pages.dev (preview branch, noindex).
- Cloudflare account: Randy's account (IDs kept out of this public repo; see Cloudflare dashboard). Zone: brewdadlabs.com.
- DNS: proxied CNAME `arcade` -> `brewdadlabs-arcade.pages.dev`. No other DNS records were touched.
- Deploy: direct upload with Wrangler from `site/`. Not git-connected.
- Source of the original HTML: `/Users/test/Documents/Arcade/BrewDadLabs Arcade.html` on Randy's Mac mini (left unchanged).

## Changes from the original HTML
- Replaced the Google Fonts `<link>` with an inline `@font-face` pointing to `/fonts/ShareTechMono-Regular.woff2` (latin subset, OFL). Nothing else changed.

## Verified (2026-11-04)
- All 4 games start in headless Chromium with no console or CSP errors.
- Zero third-party network requests; Share Tech Mono loads from the site.

## Nav back to brewdadlabs.com (LIVE)
- Randy (2026-11-04 6:19 PM ET): "the disconnect with arcade and no clear way back to the main page". The arcade had no link to brewdadlabs.com anywhere; its PROJECTS link pointed at GitHub; it lacked the main site's grid background and its footer was a joke line only.
- `site/index.html` now has a sticky header (opaque, max-width 980 like the main site): `← BREWDADLABS` brand linking to https://brewdadlabs.com/, `// ARCADE` crumb, nav HOME / PROJECTS (https://brewdadlabs.com/projects) / ARCADE (current, `#arcade`), and the SOUND button. Two rows on phones (`--hh` sets the sticky offset used by `scroll-padding-top` and `#play` `scroll-margin-top`).
- Footer: ← HOME, PROJECTS, ARCADE, ABOUT, GITHUB, "People before profit.", plus the original prompt line.
- In-arcade escapes: an `← EXIT TO THE WORKSHOP` row under the module menu, a `cd ~ ← back to brewdadlabs.com` link as the last intro line, and Matrix Terminal commands `home`/`exit`/`quit`/`logout`/`cd`/`cd ~`/`cd ..` (go to brewdadlabs.com) and `map` (go to /projects); `help` and `projects` mention them.
- Look aligned with the main site: same 44px workshop grid and vignette behind the content, 980px column, cyan focus outlines. Arcade scanlines, card colours and game visuals unchanged. Added `color-scheme: dark`. (The blank `data:` favicon was replaced by the real BrewDadLabs mark on 2026-11-05, see Favicon below.)
- No new requests; CSP unchanged.
- **Live in production** on arcade.brewdadlabs.com. Rechecked 2026-11-05 8:10 PM ET: the served page is byte-identical to `site/index.html` on `main` (9cc982a), with the `← BREWDADLABS` brand, HOME / PROJECTS / ARCADE nav and exit links. `main` is pushed (origin/main = 9cc982a); the `nav-home` branch is merged.
- Companion main-site change (ARCADE in the homepage and /projects footers) is also live on brewdadlabs.com.

## Gorillas 404 (LIVE in production, 2026-11-05 ~8:42 PM ET)
- Adds `site/404.html`: the shared BrewDadLabs Gorillas 404 game, built from `shared/gorillas-404/configs/arcade.json` in brewdadlabs-site (green on black, Share Tech Mono from `/fonts/`, "Back to BrewDadLabs Arcade" plus HOME and PROJECTS links to brewdadlabs.com).
- Unknown paths on arcade.brewdadlabs.com now return a real **404** with the Gorillas game (previously Pages fell back to `index.html` with 200). The arcade only uses `#` links, so nothing depended on that fallback.
- Single-file build; the existing CSP already allows inline script/style, so `_headers` is unchanged.
- Preview: `01209036` (branch `gorillas-404`, https://01209036.brewdadlabs-arcade.pages.dev / https://gorillas-404.brewdadlabs-arcade.pages.dev).
- **Production:** deployment `6f8df4cb-bfaa-436b-a376-a8b38acccffd` (https://6f8df4cb.brewdadlabs-arcade.pages.dev), source `f9e1c80` on branch `gorillas-404`. Curl-verified 2026-11-05 ~8:42 PM ET: `/` → 200; made-up path → 404 + Gorillas.
- Rollback: redeploy previous production `51fa1c0a-8cb2-4594-b0f4-6c1ef41f35f2` from the dashboard (or `wrangler pages deployment rollback` if available). GitHub push of `gorillas-404` → `main` is for the GitHub bot / BREWDADlabs/arcade (this bot does not push BREWDADlabs).

## Favicon (2026-11-05)
- Same mint "b" BrewDadLabs mark as brewdadlabs.com (Randy approved using the same mark on the arcade). Copied `favicon.ico` (16/32/48), `favicon-32.png`, `apple-touch-icon.png` (180) from brewdadlabs-site `site/` (commit e7d930a).
- `site/index.html`: blank `<link rel="icon" href="data:,">` replaced with the three link tags used on the main site. `site/404.html`: same three tags added.
- `/favicon.ico` now returns the icon instead of falling through to the Gorillas 404. CSP unchanged (`img-src 'self'`).
- Branch `favicon` (from `gorillas-404`). Deploy details in AI_CHANGELOG.md.

## Open items
- Optionally link https://arcade.brewdadlabs.com from the BrewDadLabs profile README.
