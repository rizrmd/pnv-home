# pnv.one — GitHub Pages Setup

This folder (`/docs`) is the publishing source for **https://pnv.one**.

## Current Setup

- **Source**: GitHub Pages is configured to deploy from the `main` branch, folder `/docs`
- **Custom domain**: `pnv.one` (configured via `CNAME` file + GitHub repo settings)
- **Static site**: Plain HTML + Tailwind (CDN) — zero build step

## How to Update the Site

1. Edit files directly in `docs/`
2. Commit and push to `main`
3. GitHub Pages will automatically redeploy (usually < 1 minute)

For larger content changes, use the **website skill**:
```
/website update the landing page
```

Drafts live in `content/website/_drafts/`. After approval, the final version should be reflected here in `docs/`.

## GitHub Pages Configuration (one-time)

Go to the repository settings:

**https://github.com/rizrmd/pnv-home/settings/pages**

1. **Source**
   - Branch: `main`
   - Folder: `/docs`

2. **Custom domain**
   - Enter: `pnv.one`
   - Check **Enforce HTTPS** after DNS propagates

3. Save.

## DNS Configuration (required for custom domain)

### For apex domain (`pnv.one`)

Add these **A records** at your DNS provider:

```
pnv.one  185.199.108.153
pnv.one  185.199.109.153
pnv.one  185.199.110.153
pnv.one  185.199.111.153
```

### Recommended (easier)

Point `www.pnv.one` via **CNAME**:

```
www  →  rizrmd.github.io
```

Then set the primary domain in GitHub to `www.pnv.one` and add a redirect from the apex if possible.

After DNS changes, it can take up to 24h (usually much faster) to fully propagate.

## Files in this folder

- `index.html` — the live landing page
- `CNAME` — tells GitHub Pages which domain to serve
- `.nojekyll` — prevents GitHub from running Jekyll processing

Do not delete `CNAME` or `.nojekyll`.

---

Last updated: 2026-05-23
Repo: https://github.com/rizrmd/pnv-home