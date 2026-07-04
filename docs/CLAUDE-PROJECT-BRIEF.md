# Quzyn — Claude Project Brief
# Paste this into your Claude Project's "Project Instructions" field

---

## What is Quzyn?

Quzyn (quzyn.com) is a map-based home-cook food ordering platform. It connects verified home chefs with neighbors who want to order authentic, culturally diverse home-cooked meals. Think of it as "Airbnb for home cooking" — but built on the Food Freedom Act, with professional food safety certification baked in.

**Parent company:** Spheronomics, Inc. · Lewisville, TX
**Co-founders:** Mansur Plumber (CTO, 75% NIB owner, formerly AdComp Systems CEO for 37 years) + Mike Wilson (CEO, retired police chief)
**Stage:** Pre-launch pilot, Dallas-Fort Worth area

---

## Platform Components (know the boundaries)

| Component | Repo | Owner | Status |
|---|---|---|---|
| Public marketing portal | `quzyn-public` | Mansur | In development |
| Cook PWA (onboarding, menu, orders) | `quzyn-cook-app` | Burhan | Partner developing |
| Buyer PWA (map, browse, order) | `quzyn-buyer-app` | Partner dev | Partner developing |
| Admin/reporting | `quzyn-admin` | Internal | Future |

**Key distinction:** The public portal hands off to the cook app for actual registration. The portal contains only the marketing pages, cottage food law reference, and CTA that links to the cook app.

---

## Brand Identity

**Logo:** House with chef's hat (uploaded — always use actual logo image, not text)
**Tagline:** "Real food. Real neighbors. Every culture."

**Colors:**
- Tomato `#D94F2B` — primary CTAs, badges
- Saffron `#F7A800` — marquee, accents, highlights
- Sage `#4A7C59` — trust indicators, verified badges, success
- Cream `#FFFDF7` — page background
- Brown `#2E1F14` — headings and body text

**Fonts:** Lora (serif display) + Nunito (body) + Caveat (handwritten accent)
**Tone:** Warm, community-driven, joyful, inclusive. Never corporate or tech-startup cold.

---

## Containers (physical product)

Quzyn supplies home chefs with three branded container types:
1. White takeout box (fold-top, wire handle)
2. Kraft eco-box (clamshell style)
3. White soup cup with lid

Every new cook gets a FREE starter kit: 25 takeout boxes + 10 soup cups + 10 kraft eco-boxes.
Container photos are uploaded and available in the repo.

---

## Quzyn Verified Cook Certification Tiers

| Tier | Requirements |
|---|---|
| 🥉 Bronze | Gov ID verified + Food Handler Cert + bank account + Food Safety Agreement signed |
| 🥈 Silver | Bronze + background check + kitchen photos + 25 orders + 4.5★ |
| 🥇 Gold | Silver + allergen training + 100 orders + 4.8★ + no safety incidents |
| ⭐ Elite | Gold + kitchen inspection + 250 orders + 4.9★ + ServSafe cert (invitation only) |

**Critical:** Food Handler Certificate is MANDATORY for ALL cooks regardless of state law. This is Quzyn's non-negotiable baseline.

---

## Trust Badges (displayed on cook profiles)

```
🟢 Food Handler Certified
🟢 Identity Verified
🟢 Background Checked
🟢 [State] Cottage Food Compliant
🟢 Kitchen Photos Verified
🟢 Allergen Training Completed
🟢 Top Rated Cook
🟢 100 Orders Completed
🟢 4.9★ Average Rating
```

---

## Cuisines Featured (representative — not exhaustive)

🇺🇸 Texas BBQ · 🇺🇸 Southern · 🇮🇹 Italian · 🇳🇬 Nigerian · 🇨🇳 Chinese · 🇹🇭 Thai · 🇻🇳 Vietnamese · 🇮🇳 Indian · 🇲🇽 Mexican · 🇱🇧 Lebanese · 🇯🇵 Japanese · 🇪🇹 Ethiopian · 🇰🇷 Korean · 🇵🇪 Peruvian · 🇬🇷 Greek · 🇲🇦 Moroccan

**Pilot chefs (illustrative):** Travis Williams (BBQ), Maria Conti (Italian), Adaeze Okonkwo (Nigerian), Wei-Lin Chen (Chinese), Mali Srisook (Thai), Linh Nguyen (Vietnamese), Priya Mehta (Indian), Debra Monroe (Southern), Nour Haddad (Lebanese)

---

## Legal & Policy Foundation

**Food Freedom Act:** Quzyn is built on the IJ Model Food Freedom Act framework.
- Source: https://ij.org/legislation/food-freedom-act/
- Key point: Allows unrestricted sale of shelf-stable homemade foods when properly labeled. Allows potentially hazardous foods with direct-to-consumer delivery.

**Launch state:** Texas (very favorable — no kitchen inspection, no revenue cap post-2023, direct sales allowed)

**Expansion priority:** Florida → Oklahoma → Wyoming → Utah → Tennessee → Arizona

**Approved training providers:** ServSafe (~$15), StateFoodSafety (~$10), eFoodHandlers (~$10)

**Revenue model:** Quzyn charges 15% platform fee. Cooks keep 85%.

---

## GitHub Structure

Organization: `github.com/spheronomics/`
Primary repo for portal work: `quzyn-public`
Branch strategy: `main` (production) → `staging` → `dev` → `feature/*`
Deployment: GitHub Pages or Netlify → quzyn.com (AWS Route 53)
Subdomains: `cook.quzyn.com` (cook app), `app.quzyn.com` (buyer app), `admin.quzyn.com`

---

## Key People

| Name | Role | Notes |
|---|---|---|
| Mansur Plumber | CTO & Co-Founder | Decision maker, full stack context |
| Mike Wilson | CEO & Co-Founder | Retired police chief, community relationships |
| Burhan | Lead Dev | eCitation developer, will scaffold cook app repo |

---

## What Claude should always do in this project

1. **Use the actual Quzyn logo** in any HTML/design work — never substitute text or emoji
2. **Show real food photography** (Unsplash CDN URLs) — no emoji as food stand-ins
3. **Maintain brand colors exactly** — use the CSS variables from `src/styles/variables.css`
4. **Reference the four container types** when discussing packaging
5. **Always include the free starter kit** messaging in cook-facing content
6. **Food Handler Certificate = mandatory** — never suggest it's optional
7. **Keep portal vs. cook app boundaries clear** — registration flow lives in the cook app
8. **File output paths:** HTML → `/mnt/user-data/outputs/`, docs → reference inline

---

## Current Development State (July 2025)

- ✅ Main marketing site (quzyn-v5.html) — complete, needs real chef photos
- ✅ Chef registration page (quzyn-register.html) — complete
- ✅ GitHub repo structure — scaffolded
- 🔄 Google Workspace setup — in progress (quzyn.com domain, hello@quzyn.com)
- 🔄 Cook app — Burhan / partner developing (PWA)
- ⏳ Buyer app — partner developing
- ⏳ Cottage food law reference page — designed, needs build
- ⏳ Press outreach — draft press release ready
- ⏳ Celebrity/advocate outreach — targets identified (Tabitha Brown, Carla Hall, José Andrés, etc.)
- ⏳ Pilot chef recruitment — DFW area
