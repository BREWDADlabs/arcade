# AI Handoff

_Last updated: 2026-11-04 (America/New_York)_

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

## Open items
- Optionally link https://arcade.brewdadlabs.com from the BrewDadLabs profile README.
