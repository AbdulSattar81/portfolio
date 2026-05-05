# Abdul Sattar Mohammed — Portfolio

A single-file, zero-build, recruiter-grade portfolio for a Cloud / DevOps engineer.

## Structure

```
portfolio/
├── index.html                          # the entire site (HTML + CSS + JS, single file)
├── README.md
├── robots.txt
├── sitemap.xml
├── .gitignore
├── .github/
│   └── workflows/
│       └── deploy.yml                  # auto-deploy to GitHub Pages on push to main
└── assets/
    ├── docs/
    │   └── abdul-sattar-resume.pdf     # ← drop your résumé here (filename matters)
    └── img/
        └── og-cover.png                # ← optional 1200×630 social share image
```

## Run locally

No build step. No dependencies. Open it.

```bash
# any one of these:
python3 -m http.server 8080
npx serve .
open index.html
```

## Deploy

### Option A — GitHub Pages (recommended, free, auto-deploys)

```bash
git init
git add .
git commit -m "feat: portfolio v2"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo>.git
git push -u origin main
```

In the repo: **Settings → Pages → Source: GitHub Actions**. The workflow in `.github/workflows/deploy.yml` will build and ship on every push to `main`. First deploy takes ~1 min.

For a custom domain (e.g. `sattar.cloud`): add a `CNAME` file containing your domain at the repo root, and point a CNAME DNS record at `<username>.github.io`.

### Option B — AWS S3 + CloudFront (the on-brand move)

```bash
aws s3 sync . s3://your-bucket-name \
  --exclude ".git/*" --exclude ".github/*" --exclude "README.md" \
  --cache-control "public, max-age=300"

aws cloudfront create-invalidation \
  --distribution-id <DIST_ID> --paths "/*"
```

Bucket should have static-website hosting enabled, CloudFront origin pointed at it, ACM cert in `us-east-1`, and a Route 53 alias.

### Option C — Netlify / Vercel / Cloudflare Pages (drag-and-drop)

Drag the entire `portfolio/` folder onto netlify.com/drop. Done.

## Before you publish — checklist

- [ ] Drop `abdul-sattar-resume.pdf` into `assets/docs/`
- [ ] Replace GitHub URL in `index.html` (search for `github.com/abdulsattar`) with your actual handle
- [ ] Replace LinkedIn URL (search for `linkedin.com/in/abdulsattar`) with your actual handle
- [ ] Update `<link rel="canonical" href="https://sattar.cloud/" />` to your real domain
- [ ] (Optional) Drop a 1200×630 OG image at `assets/img/og-cover.png` and uncomment the `og:image` meta tag
- [ ] Test the command palette: press `⌘K` (Mac) or `Ctrl+K` (Win/Linux)
- [ ] Test the theme toggle (sun/moon icon, top-right)
- [ ] Open in mobile view — single-column hero, accessible nav

## Stack

- **Markup:** semantic HTML5 with JSON-LD `Person` schema, OG/Twitter meta, inline SVG favicon
- **Styles:** CSS custom properties, container queries-friendly, dual theme (dark default + light), print stylesheet
- **Scripts:** vanilla JS (~250 lines) — no React, no Tailwind, no build pipeline
- **Type:** Manrope (sans), Instrument Serif (italic accents), JetBrains Mono (technical metadata)
- **Browser support:** evergreen (Chrome / Safari / Firefox / Edge ≥ 2 versions)

## License

All content © Abdul Sattar Mohammed. Code structure free to fork; replace content with yours.
