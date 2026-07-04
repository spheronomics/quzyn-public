# Quzyn Platform Architecture

## Overview

Quzyn is composed of four distinct applications. This document explains how `quzyn-public` fits into the broader platform and where responsibilities are divided.

```
┌─────────────────────────────────────────────────────────────┐
│                        quzyn.com                            │
│                    (public portal)                          │
│              repo: quzyn-public  ← THIS REPO               │
│                                                             │
│  • Marketing site          • Cottage food law reference     │
│  • Cook registration CTA   • Press / media kit              │
│  • About / legal pages     • Waitlist capture               │
└──────────────────┬──────────────────────────────────────────┘
                   │  hands off to →
      ┌────────────┴──────────────┐
      │                           │
      ▼                           ▼
┌─────────────┐          ┌──────────────────┐
│  Cook App   │          │   Buyer App      │
│  (PWA)      │          │   (PWA)          │
│             │          │                  │
│ • Registration          │ • Map browse     │
│ • Onboarding            │ • Chef profiles  │
│ • Menu mgmt             │ • Order & pay    │
│ • Order mgmt            │ • Track orders   │
│ • Earnings              │ • Reviews        │
│ • Badge display         │                  │
│                         │                  │
│ repo: quzyn-cook-app    │ repo: quzyn-buyer-app │
│ owner: Burhan / dev     │ owner: partner dev    │
└─────────────┘          └──────────────────┘
      │                           │
      └────────────┬──────────────┘
                   │
                   ▼
          ┌─────────────────┐
          │   Admin / Ops   │
          │                 │
          │ • Verification  │
          │ • Reporting     │
          │ • Chef mgmt     │
          │ • Analytics     │
          │                 │
          │ repo: quzyn-admin│
          └─────────────────┘
```

---

## Data Flow: Cook Registration

```
quzyn.com/register
    │
    │  (user fills basic info + selects state)
    │
    ▼
Cook App Registration Flow (quzyn-cook-app)
    │
    ├── Step 1: Personal info
    ├── Step 2: State compliance check (Quzyn Compliance Engine API)
    ├── Step 3: Food Handler Certificate upload → S3 + manual review queue
    ├── Step 4: ID upload → Stripe Identity or equivalent
    ├── Step 5: Background check → 3rd party screener
    ├── Step 6: Kitchen photos → S3
    ├── Step 7: Bank account → Stripe Connect
    └── Step 8: Agreement → signed + timestamped → database
    │
    ▼
Admin Review Queue
    │
    ├── Certificate verified → badge unlocked → Bronze tier granted
    ├── Container kit order triggered → fulfillment partner
    └── Chef profile goes live on map
```

---

## Hosting & Infrastructure

| Service | Provider | Notes |
|---|---|---|
| Public portal hosting | GitHub Pages or Netlify | Auto-deploy from `main` |
| Domain | AWS Route 53 | quzyn.com already configured |
| Cook/Buyer apps | AWS (EC2 / Lightsail) | Existing NIB infrastructure pattern |
| File storage | AWS S3 | Certificate uploads, kitchen photos |
| Payments | Stripe Connect | Cook payouts + buyer checkout |
| Email | AWS SES | Transactional (hello@quzyn.com via Google Workspace for human email) |
| CDN | CloudFront (or Netlify CDN) | Static assets |

---

## GitHub Organization Structure

```
github.com/spheronomics/
├── quzyn-public        ← This repo (public portal)
├── quzyn-cook-app      ← Cook PWA (Burhan)
├── quzyn-buyer-app     ← Buyer PWA (partner dev)
├── quzyn-admin         ← Internal ops & reporting
└── quzyn-api           ← Shared backend API (future)
```

---

## Environment Variables (public portal)

The public portal is static HTML — no environment variables needed for the marketing site itself. If JavaScript API calls are added (e.g., waitlist form POSTing to a backend):

```
QUZYN_API_URL=https://api.quzyn.com
QUZYN_WAITLIST_ENDPOINT=/v1/waitlist
```

Store in Netlify environment settings or GitHub Actions secrets — never commit to the repo.

---

## Branch Strategy

```
main          ← production (auto-deploys to quzyn.com)
staging       ← pre-production review
dev           ← active development
feature/*     ← individual features (PR into dev)
hotfix/*      ← urgent production fixes (PR into main)
```

---

## Cook App Handoff Points

The public portal hands off to the cook app at these URLs:

| Public portal link | Cook app destination |
|---|---|
| `quzyn.com/register` | `cook.quzyn.com/onboarding/start` |
| "Join as a cook" CTA | `cook.quzyn.com/signup` |
| "Claim free kit" button | `cook.quzyn.com/onboarding/start?ref=freekit` |
| Chef profile links | `cook.quzyn.com/profile/{id}` |

Coordinate subdomain with Burhan: `cook.quzyn.com` → cook app, `app.quzyn.com` → buyer app.
