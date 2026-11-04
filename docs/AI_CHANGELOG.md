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
