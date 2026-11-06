# AI Changelog

## 2026-11-04
- Created Cloudflare Pages project `brewdadlabs-arcade` (production branch `main`).
- Added `site/index.html` from Randy's BrewDadLabs Arcade.html; swapped Google Fonts for self-hosted Share Tech Mono (`site/fonts/`, OFL).
- Added `site/_headers`: CSP, nosniff, Referrer-Policy, X-Frame-Options DENY; `X-Robots-Tag: noindex` on `*.pages.dev` only.
- Deployed preview, verified games, then deployed to production.
- Attached custom domain arcade.brewdadlabs.com; created proxied CNAME `arcade` -> `brewdadlabs-arcade.pages.dev`.
- Created this repo with README, AGENTS.md, and these docs.

## 2026-11-04 4:30 PM ET, GitHub bot
- **Goal:** publish the arcade source as the public repo BREWDADlabs/arcade, at Randy's request.
- **Files:** docs/AI_HANDOFF.md, docs/AI_CHANGELOG.md
- **Summary:** removed the Cloudflare account, zone and DNS record IDs from the handoff before the first public push. They aren't secrets, but they don't belong in a public repo. Folded into the initial commit, which had never been pushed.
- **Tests:** secrets scan of every tracked file was clean, with no 32-hex IDs left.
- **Deploy:** none. The site is deployed separately with Wrangler (Websites bot).
- **Rollback:** revert the commit.

## 2026-11-04 6:27 PM ET, Websites bot (nav back to brewdadlabs.com, preview)
- **Goal:** Randy: "the disconnect with arcade and no clear way back to the main page".
- **Files:** site/index.html, docs/AI_HANDOFF.md, docs/AI_CHANGELOG.md
- **Summary:** sticky header with `← BREWDADLABS` brand + HOME / PROJECTS / ARCADE nav linking to brewdadlabs.com; matching footer links; `← EXIT TO THE WORKSHOP` row under the module menu; intro ends with a link home; Matrix Terminal `home`/`exit`/`cd ~` and `map` commands; main-site grid background, vignette and 980px column; data: favicon. Games untouched.
- **Tests:** headless Chromium (system Chrome) at 1280x800 and 390x844, local and on the preview: zero third-party requests, no console or page errors, brand link visible at top, during each of the 4 games and at the bottom, and it navigates to https://brewdadlabs.com/ (click and tap); terminal `home` navigates there too; Snake responds to arrows (no page scroll) and `p` pauses; Matrix `help` lists home; Circuit tile rotates on click/tap; Defender moves/fires on keys and the touch pad; Escape closes a game; game stage sits below the sticky header.
- **Deploy:** preview branch only (https://preview.brewdadlabs-arcade.pages.dev). No production deploy, no push.
- **Rollback:** delete branch `nav-home`; production is untouched.

## 2026-11-05 8:15 PM ET, Websites bot (docs: nav is live)
- **Goal:** Randy: update the repo notes that still said the nav changes were "preview only".
- **Files:** docs/AI_HANDOFF.md, docs/AI_CHANGELOG.md
- **Summary:** the nav back to brewdadlabs.com is live on arcade.brewdadlabs.com; handoff now says so. Checked with curl: the live page matches `site/index.html` at 9cc982a.
- **Deploy:** none (docs only).

## 2026-11-05 8:20 PM ET, Websites bot (Gorillas 404, branch, not deployed)
- **Goal:** Randy: roll the Gorillas 404 out to every site.
- **Files:** site/404.html, docs/AI_HANDOFF.md, docs/AI_CHANGELOG.md
- **Summary:** added the shared Gorillas 404 built from brewdadlabs-site `shared/gorillas-404/configs/arcade.json`.
- **Tests:** headless Chrome 1280x800 and 390x844, live CSP: 404 status, game runs and throws, no CSP errors, no third-party requests.
- **Deploy:** none. Needs Randy's OK (preview, then production).
- **Rollback:** delete `site/404.html` and redeploy, or redeploy the previous deployment.

## 2026-11-05 ~8:42 PM ET, Websites bot (Gorillas 404 → production)
- **Goal:** Randy approved (widget t162s651 / ask t162u): ship Gorillas 404 to production on arcade (among others).
- **Files:** docs only here (site/404.html was already on branch `gorillas-404` @ f9e1c80).
- **Deploy:** production `6f8df4cb-bfaa-436b-a376-a8b38acccffd` via `wrangler pages deploy ./site --project-name=brewdadlabs-arcade --branch=main` from Mac (`f9e1c80`). Preview was `01209036`.
- **Tests:** curl arcade.brewdadlabs.com `/` → 200 (Arcade title); made-up path → 404 with Gorillas markers.
- **Rollback:** previous production `51fa1c0a-8cb2-4594-b0f4-6c1ef41f35f2`.
- **Git:** no BREWDADlabs push from this bot; GitHub bot can merge `gorillas-404` → `main` when ready.
