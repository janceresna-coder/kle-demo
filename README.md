# Kaufland Listing Engine — demo site

Single-file static demo of the KLE web UI. No backend; everything is
client-side mocked. Used internally at EXPANDO to show the engine to
colleagues without standing up a full deploy.

## Files

- `index.html` — the entire demo (≈ 34 KB, no build step)
- `vercel.json` — minimal static hosting config: clean URLs, security
  headers, light caching on the index

## Local preview

Just open `index.html` in a browser. No server needed.

```bash
# or, optionally:
python3 -m http.server -d . 8000
# then open http://localhost:8000
```

## Deploy on Vercel

1. Push this folder to a new GitHub repo (public or private — both work).
2. https://vercel.com/new → Import the GitHub repo → leave all defaults.
3. Vercel detects no framework and serves `index.html` at the root.
4. URL appears in seconds: `https://<repo-name>-<hash>.vercel.app`.

Updates: any push to `main` triggers an automatic redeploy.

## Custom domain

In the Vercel project: **Settings → Domains → Add** → enter e.g.
`kle-demo.expan.do`. Vercel shows the CNAME / A record values to point
your DNS at. Once the DNS propagates (usually under 5 min), the demo is
live at the custom URL with automatic HTTPS.

## What the demo shows

- Dashboard with stub Fightstore data (3 BJJ Gi variants)
- Working filter pills (All / Live / Pending / Error / Dry run)
- Dry-run and Publish buttons that mutate state + show toasts
- Upload form accepting CSV, XLSX, or BaseLinker-style XML
- Real client-side parsers (PapaParse, SheetJS, browser DOMParser)
- Full GTIN/ISBN-10 check-digit validation with scientific-notation
  detection — ported 1:1 from the real Python engine's `kle.parsing.ean`

## What the demo does NOT include

- Real Kaufland Seller API calls
- Real persistence (refresh wipes state)
- Authentication / multi-tenant credentials
- Background stock + price sync (APScheduler)
- Per-category attribute schema validation

Those all live in the actual `kaufland-listing-engine` Python project.
