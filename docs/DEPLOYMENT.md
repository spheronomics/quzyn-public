# Quzyn Public Portal — Deployment Guide

## Overview

The public portal is a static HTML/CSS/JS site. No build step, no framework, no Node.js required. Deployable in minutes.

---

## Option A: GitHub Pages (Recommended to start)

### One-time setup

1. Push `quzyn-public` repo to GitHub under the `spheronomics` organization
2. Go to repo Settings → Pages
3. Source: Deploy from branch `main` → folder `/` (root) or `/src`
4. GitHub will publish at: `spheronomics.github.io/quzyn-public`

### Connect quzyn.com domain

In your AWS Route 53 hosted zone for `quzyn.com`, add:

```
Type: CNAME
Name: www
Value: spheronomics.github.io
TTL: 300
```

For apex domain (`quzyn.com` without www), add these A records pointing to GitHub Pages IPs:

```
Type: A  →  185.199.108.153
Type: A  →  185.199.109.153
Type: A  →  185.199.110.153
Type: A  →  185.199.111.153
```

Then in GitHub Pages settings, set custom domain to `quzyn.com`.

**HTTPS:** GitHub Pages provisions a free Let's Encrypt certificate automatically. Enable "Enforce HTTPS."

---

## Option B: Netlify (Better for forms + future functions)

### Deploy

```bash
# Install Netlify CLI
npm install -g netlify-cli

# From repo root
netlify login
netlify init
netlify deploy --prod --dir=src
```

### Connect domain

In Netlify: Site settings → Domain management → Add custom domain → `quzyn.com`

In AWS Route 53, update nameservers to Netlify's NS records (Netlify provides these).

**Advantage of Netlify:** Built-in form handling (waitlist form submissions work without a backend), redirects, and edge functions for future dynamic features.

---

## Auto-Deploy via GitHub Actions

File: `.github/workflows/deploy.yml`

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./src
```

Every push to `main` auto-deploys. Typically live within 2 minutes.

---

## Environment Checklist Before Go-Live

- [ ] quzyn.com DNS records updated in Route 53
- [ ] HTTPS enforced (auto via GitHub Pages / Netlify)
- [ ] Google Workspace MX records in place (hello@quzyn.com live)
- [ ] Google Analytics or Plausible added to all pages
- [ ] Waitlist form connected to backend or Netlify Forms
- [ ] `hello@quzyn.com` monitored
- [ ] Quzyn logo assets in `/src/assets/images/`
- [ ] Container photos in `/src/assets/images/containers/`
- [ ] Meta tags, OG images, and favicon set on all pages
- [ ] Mobile tested on iOS Safari and Android Chrome
- [ ] Page speed tested (Lighthouse score > 90)

---

## Subdomain Plan (coordinate with Burhan)

| Subdomain | Points to | Purpose |
|---|---|---|
| `quzyn.com` | GitHub Pages | Public marketing portal |
| `www.quzyn.com` | GitHub Pages | Alias |
| `cook.quzyn.com` | Cook app server | Cook PWA |
| `app.quzyn.com` | Buyer app server | Buyer PWA |
| `admin.quzyn.com` | Admin server | Internal ops |
| `api.quzyn.com` | API server | Shared backend (future) |

All subdomains managed in Route 53 hosted zone `quzyn.com`.
