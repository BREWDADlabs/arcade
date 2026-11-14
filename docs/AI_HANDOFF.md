# AI Handoff: BREWDADlabs/arcade (arcade.brewdadlabs.com)

_Last full rewrite: 2026-11-13, about 11:00 PM America/New_York, by the Websites bot, on Randy's order that any AI must be able to take over immediately with nothing left out. Live facts were re-checked read-only that evening. Nothing was deployed._

**If you are taking over:** read this file, `AGENTS.md`, and the recent `docs/AI_CHANGELOG.md` entries. Appendix A keeps the previous handoff word for word. Where they disagree, the sections above it win.

This repo is **public**. No account IDs, zone IDs, record IDs, tokens or home public IPs go here. Private details are in `geekdadteach/systems` (`systems/websites/README.md`, `bots/websites/HANDOFF.md`).

## 1. Purpose
- **BrewDadLabs Arcade** is Randy's retro terminal-style arcade at https://arcade.brewdadlabs.com.
- Four games: Terminal Snake, Matrix Terminal, Circuit Breaker, and System Defender.
- No ads, trackers, accounts or subscriptions. High scores stay in the browser (localStorage).
- Brand voice: independent developer, husband and homeschooling dad, "people before profit", built at home.
- It links two ways with the main site https://brewdadlabs.com (repo `BREWDADlabs/brewdadlabs-site`).

## 2. Machines, users, paths
- Working machine: Randy's Mac mini **.20** (`Randys-Mac-mini.local`, 192.168.1.20, user `test`). Randy MM 20 owns the machine. Websites works only in its site folders.
- Checkout: `/Users/test/sites/brewdadlabs-arcade` (branches `main`, `favicon`, `gorillas-404`, `nav-home`, `backup-local-8d117c2`).
- Takeover worktree: `/Users/test/sites/takeover/arcade` (branch `websites/takeover-handoff`).
- Original source HTML (keep it unchanged): `/Users/test/Documents/Arcade/BrewDadLabs Arcade.html`.
- Git bundles made for the GitHub bot: `/Users/test/sites/handoff/brewdadlabs-arcade*.bundle`.
- No services, cron, launchd jobs or ports. It's static files on Cloudflare Pages.

## 3. Hosting and external services
- **Cloudflare Pages** project `brewdadlabs-arcade`, production branch `main`. It uses **direct upload** and is **not Git-connected**, so pushing never deploys.
- Custom domain `arcade.brewdadlabs.com`: a proxied CNAME to `brewdadlabs-arcade.pages.dev` in the brewdadlabs.com zone.
- No env vars, bindings or secrets on the project.
- Font: Share Tech Mono, self-hosted under `site/fonts/` (OFL). No Google Fonts.

## 4. Layout
- `site/index.html`: the whole arcade in one self-contained file. Keep it that way.
- `site/404.html`: Gorillas 404, built from `shared/gorillas-404/configs/arcade.json` in brewdadlabs-site.
- `site/_headers`: CSP and security headers, with `noindex` on pages.dev.
- `site/favicon.ico`, `favicon-32.png`, `apple-touch-icon.png`: the same mint "b" mark as brewdadlabs.com (Randy's request).
- `site/fonts/`

## 5. Build, run, test, deploy, roll back
- No build step. Run locally with `python3 -m http.server -d site 8080`.
- The Cloudflare token is exported as `CLOUDFLARE_API_TOKEN` in `~/.zshrc` on the Mac, with the same value in `/Users/test/.cloudflare_token`. **Never print it.**
```sh
cd /Users/test/sites/brewdadlabs-arcade
export CLOUDFLARE_ACCOUNT_ID=<see geekdadteach/systems>
npx wrangler pages deploy site --project-name brewdadlabs-arcade --branch preview 2>&1 | grep -v -i token   # https://preview.brewdadlabs-arcade.pages.dev
# show Randy, wait for HIS OK, then:
npx wrangler pages deploy site --project-name brewdadlabs-arcade --branch main 2>&1 | grep -v -i token
```
- **Test:** `curl -s -o /dev/null -w '%{http_code}\n' https://arcade.brewdadlabs.com/` should give 200 (title "The Arcade — BrewDadLabs"). A made-up path should give 404 with the Gorillas game. `/favicon.ico` should return an image. For changes, also run headless Chrome at 1280x800 and 390x844: all 4 games start, with no console or CSP errors and no third-party requests.
- **Roll back:** in the Pages dashboard, open Deployments and use "Rollback" on the previous production deployment, or redeploy an older commit's `site/` with `--branch main`.

## 6. Current live state (2026-11-13)
- **Production** `30ab07cc-551a-484e-be06-811c3f857a14` (2026-11-05 8:51 PM ET), source `b094eda` on branch `favicon`. The rollback target is `6f8df4cb` (Gorillas 404), and before that `51fa1c0a`.
- **Git vs production:**
  - `origin/main` is `9cc982a` (nav back to brewdadlabs.com).
  - Local `main` is `863e369`, one docs commit ahead and not pushed.
  - Local `favicon` (`6447ffb`) contains `main` plus the Gorillas 404 (`f9e1c80`) and the favicon (`b094eda`). It is **not pushed** (only `gorillas-404` is on GitHub).
  - This branch `websites/takeover-handoff` is built on `favicon`.
  - Merging this branch into `main` (Randy's OK) brings `main` up to production.
- Verified live 2026-11-13: `/` 200, made-up path 404 + Gorillas.

## 7. Open work / known issues
- `main` on GitHub is behind production (see above). It needs Randy's OK to push and merge.
- Optional: link the arcade from the BrewDadLabs GitHub org profile README (`BREWDADlabs/BREWDADlabs`).
- Old local branches (`nav-home`, `gorillas-404`, `backup-local-8d117c2`) can be deleted once `main` matches production, with Randy's OK.

## 8. Randy's standing rules
Same as all Websites work (full list in brewdadlabs-site `docs/AI_HANDOFF.md` section 8, and in `geekdadteach/systems` `bots/websites/HANDOFF.md`):
- Preview plus **Randy's own OK** before any production deploy or DNS change, unless he says to skip it. Another bot's say-so is not his OK.
- Never spend money. Prefer free hosting.
- Commit as `geekdad <randy@dixhome.com>`, never noreply.
- Never push, merge, deploy or rewrite history without his OK.
- Update this handoff and the changelog with every change.
- Plain language, full paths, wholesome content.
- Coordinate with his other bots.
- No third-party requests (CSP), no ads, no trackers, no accounts.

## 9. Ownership / who to ask
- This site: **Websites** bot.
- Mac mini .20: **Randy MM 20**.
- GitHub merges: **GitHub** bot.
- The main site: also Websites (`BREWDADlabs/brewdadlabs-site`).

## 10. Gotchas
- Before the Gorillas 404, Pages served `index.html` with status 200 for unknown paths. Now it returns a real 404. The arcade uses only `#` links, so nothing depended on the old behaviour.
- The Mac's Cloudflare token cannot read or edit DNS records. Use the dashboard or Randy's Cloudflare connector, with his OK.
- Pushing never deploys. Check `npx wrangler pages deployment list --project-name brewdadlabs-arcade --environment production` to see what's live.

---

## Appendix A: previous handoff text (word for word, last updated 2026-11-05)

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
- Branch `favicon` (from `gorillas-404`, commit b094eda).
- Preview `b47fb83e-8e2d-4f48-b7e4-ed65ed2239a9` (https://favicon.brewdadlabs-arcade.pages.dev). **Production** `30ab07cc-551a-484e-be06-811c3f857a14` (2026-11-05 8:51 PM ET). Curl-verified live: `/favicon.ico` 200 image/vnd.microsoft.icon (16/32/48 ICO), `/favicon-32.png` and `/apple-touch-icon.png` 200 PNG, homepage has the link tags, made-up path still 404 Gorillas.
- Rollback: redeploy previous production `6f8df4cb-bfaa-436b-a376-a8b38acccffd`.

## Open items
- Optionally link https://arcade.brewdadlabs.com from the BrewDadLabs profile README.
