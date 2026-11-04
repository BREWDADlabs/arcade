# AGENTS.md

Notes for AI agents and helpers working in this repo.

- Site content lives in `site/`. `site/index.html` is the whole arcade; keep it a single self-contained file.
- Do not add third-party requests (CDNs, analytics, Google Fonts). The CSP in `site/_headers` blocks them on purpose.
- Keep content wholesome. No ads, trackers, or accounts.
- Deploy is Cloudflare Pages direct upload (project `brewdadlabs-arcade`, production branch `main`). Pushing to GitHub does not deploy.
- Preview first (`--branch preview`), get Randy's OK, then deploy `--branch main`.
- Never commit API tokens or secrets.
- Update `docs/AI_HANDOFF.md` and `docs/AI_CHANGELOG.md` with every change.
