# Quzyn — Public Portal

> **Real food. Real neighbors. Every culture.**
> Quzyn connects home chefs with hungry neighbors through a map-based food ordering platform — built on the principles of the Food Freedom Act and cottage food entrepreneurship.

---

## Repository Overview

This repo (`quzyn-public`) contains the **public-facing marketing portal** for Quzyn — the website, landing pages, cottage food law reference, cook registration landing, and supporting marketing assets.

> **What this repo is NOT:**
> The PWA buyer app, cook app, and reporting/admin pages are maintained in separate repos by the Quzyn development team. The cook registration *flow* (multi-step onboarding, document upload, verification) is part of the cook app. This repo contains only the public landing page shell that hands off to the cook app.

---

## Repo Structure

```
quzyn-public/
├── src/
│   ├── pages/
│   │   ├── index.html              # Main marketing site (quzyn.com)
│   │   ├── register.html           # Cook registration landing → hands off to cook app
│   │   ├── cottage-food-laws.html  # State-by-state cottage food law reference
│   │   ├── about.html
│   │   ├── privacy.html
│   │   └── terms.html
│   ├── components/
│   │   ├── nav.html
│   │   ├── footer.html
│   │   └── chef-card.html
│   ├── styles/
│   │   ├── main.css
│   │   ├── variables.css           # Brand tokens (colors, fonts, spacing)
│   │   └── components.css
│   └── assets/
│       ├── images/
│       │   ├── quzyn-logo.png
│       │   ├── containers/         # Product container photography
│       │   └── chefs/              # Chef profile photos (pilot)
│       ├── fonts/
│       └── icons/
├── marketing/
│   ├── press/                      # Press releases, media kit
│   ├── social/                     # Social media assets & copy
│   └── email-campaigns/            # Waitlist & launch email templates
├── legal/
│   ├── food-safety-agreement.md    # Quzyn Cook Food Safety Standards
│   ├── terms-of-service.md
│   └── privacy-policy.md
├── docs/
│   ├── BRAND.md                    # Brand guide (colors, fonts, tone)
│   ├── ARCHITECTURE.md             # How this repo fits into Quzyn's stack
│   ├── COTTAGE-FOOD-LAWS.md        # Research notes for law reference page
│   └── DEPLOYMENT.md               # How to deploy to production
├── scripts/
│   └── deploy.sh                   # Deploy to GitHub Pages / Netlify
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug-report.md
│   │   ├── content-update.md
│   │   └── new-feature.md
│   └── workflows/
│       └── deploy.yml              # CI/CD: auto-deploy on push to main
├── .gitignore
└── README.md
```

---

## Tech Stack

| Layer | Choice | Why |
|---|---|---|
| Hosting | GitHub Pages or Netlify | Free, fast CDN, deploys on push |
| HTML/CSS | Vanilla (no framework) | Fast load, no build step needed for static pages |
| Fonts | Google Fonts (Lora + Nunito) | Brand typography |
| Images | Optimized WebP + Unsplash CDN | Performance |
| CI/CD | GitHub Actions | Auto-deploy on merge to `main` |
| Domain | quzyn.com (AWS Route 53) | Already configured |

---

## Related Repositories

| Repo | Owner | Description |
|---|---|---|
| `quzyn-public` | Mansur / Portal team | This repo — public marketing site |
| `quzyn-cook-app` | Burhan / Dev team | Cook PWA: registration, menu mgmt, orders |
| `quzyn-buyer-app` | Partner dev team | Buyer PWA: map, browse, order, track |
| `quzyn-admin` | Internal | Reporting, dashboards, ops |

---

## Brand Quick Reference

- **Primary:** Tomato `#D94F2B` — CTAs, badges, alerts
- **Accent:** Saffron `#F7A800` — marquee, highlights, marquee band
- **Sage:** `#4A7C59` — trust indicators, verified badges
- **Cream:** `#FFFDF7` — background
- **Brown:** `#2E1F14` — headings, body text
- **Display font:** Lora (serif) — headlines
- **Body font:** Nunito (sans) — body, UI
- **Handwritten accent:** Caveat — eyebrows, tags

---

## Getting Started (Local Dev)

```bash
git clone https://github.com/spheronomics/quzyn-public.git
cd quzyn-public
# No build step needed — open src/pages/index.html in browser
# Or use Live Server in VS Code for hot reload
```

---

## Deployment

**Automatic:** Push to `main` → GitHub Actions runs → deploys to GitHub Pages at `quzyn.com`

**Manual:**
```bash
bash scripts/deploy.sh
```

See `docs/DEPLOYMENT.md` for DNS configuration with AWS Route 53.

---

## Contributing

1. Create a branch: `git checkout -b feature/your-feature-name`
2. Make changes
3. Open a Pull Request against `main`
4. Requires 1 review before merge

See `.github/ISSUE_TEMPLATE/` for bug reports, content updates, and feature requests.

---

## Legal & Compliance

Quzyn operates under the Food Freedom Act framework. For legal reference material see `legal/` and `docs/COTTAGE-FOOD-LAWS.md`.

> Quzyn is a product of **Spheronomics, Inc.** · Lewisville, TX
> Contact: hello@quzyn.com
