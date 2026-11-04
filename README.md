# BrewDadLabs Arcade

Retro terminal games that run in your browser. One HTML file, no build step.

**Play:** https://arcade.brewdadlabs.com

## Games

1. **Terminal Snake** – classic Snake, green phosphor edition.
2. **Matrix Terminal** – falling code with a working terminal. Try `privacy`.
3. **Circuit Breaker** – rotate tiles to connect the source to the output.
4. **System Defender** – protect the workshop from bugs and rogue packets.

## Privacy

- No ads, no trackers, no accounts, no subscriptions.
- High scores stay in your browser's localStorage. Nothing is sent anywhere.
- The font is hosted here, not loaded from Google. The page makes no third-party requests.

## What's in here

- `site/index.html` – the whole arcade.
- `site/_headers` – security headers (CSP, nosniff, no framing). `*.pages.dev` hosts get `noindex`.
- `site/fonts/` – Share Tech Mono, licensed under the SIL Open Font License 1.1 (`OFL.txt`).

## Deploy

Hosted on Cloudflare Pages by direct upload. The Pages project is **not** connected to this repo, so pushing does not deploy.

```
npx wrangler pages deploy site --project-name brewdadlabs-arcade --branch main
```

Use `--branch preview` to test first at https://preview.brewdadlabs-arcade.pages.dev.

Built at home. People before profit.
