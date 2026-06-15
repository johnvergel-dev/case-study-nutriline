# Nutriline Corp — Case Study

> **Precision poultry-nutrition company** · corporate website + private admin platform, built end-to-end.
> 🌐 **Live:** https://nutrilinecorp.com  ·  📍 Ambato, Ecuador

<p align="center"><img src="docs/home.jpg" alt="Nutriline Corp — homepage" width="900"></p>

| | |
|---|---|
| **Role** | Solo full-stack developer (freelance) |
| **Client** | Nutriline Corp — poultry-nutrition & feed-additives manufacturer |
| **Industry** | B2B · animal nutrition / agribusiness |
| **Stack** | Next.js 14 · React 18 · Tailwind CSS · Sequelize / MySQL · framer-motion |
| **Status** | Live in production |

---

## Overview
Nutriline Corp needed to go from no real web presence to a credible, fast, **self-manageable** platform — one site that works as a sales storefront for the public *and* a private back-office for the team. I designed and built it solo: front-end, back-end, database, deployment and SEO.

## The client & the brief
Nutriline Corp is an Ecuadorian manufacturer specialised in **precision poultry nutrition**. Their catalog covers the inputs feed mills and poultry farms use to optimise broiler and layer performance: **amino acids** (L-Lysine, L-Threonine), **choline chloride**, **monocalcium phosphate**, **minerals & vitamins**, **additives** and **custom premixes**.

Their customers are **B2B** — feed producers, distributors and farms — so the site has to do four jobs at once:
1. **Build trust** with a professional, certified-looking presence (the industry runs on credibility and certifications like GMP).
2. **Showcase the catalog** with real technical detail per product.
3. **Be found** — rank for poultry-nutrition searches and be citable by AI assistants.
4. **Be self-served** — the team adds/edits products and reads leads without a developer.

## What the site includes
A single Next.js application serves both a public website and a private admin panel from one deployment.

### Public site
- **Home** — brand hero ("Nutrición y Bienestar Avícola"), value pillars (certified technology, sustainable processes, national coverage), featured products and a "Hablemos de tu Proyecto" contact funnel.
- **Products** — a catalog filterable by category (**Supplements & Additives · Minerals & Vitamins · Premixes · Raw materials**). Each product has its own **server-rendered detail page** (`/products/[slug]`) with a technical sheet, benefits and price. Lines live on the site today include:

  | Product | Category | Price |
  |---|---|---|
  | L-Lysine HCl 98.5% | Amino acid | $50 |
  | Choline Chloride 60% (plant-based) | Additive | $28 |
  | L-Threonine 98.5% | Amino acid | $50 |
  | Monocalcium Phosphate 22.7% (Greenphos) | Mineral | $32.50 |
- **Resources** — a technical library of articles for poultry producers (a long-term SEO engine).
- **About / Contact** — company information and a rate-limited contact form that lands leads in the admin inbox.

### Admin panel (`/admin`)
An authenticated dashboard so the Nutriline team runs the site themselves:
- Create / edit / activate products — new products appear instantly, no rebuild.
- Manage the technical resources library.
- Read and triage messages from the contact form.

## Screenshots
<p align="center">
  <img src="docs/products.jpg" alt="Product catalog" width="49%">
  <img src="docs/full.jpg" alt="Full homepage" width="49%">
</p>

## The challenge
The site runs on **shared hosting** (no Next.js image optimizer, a single Node process via Passenger), and the first version was a client-rendered app behind a ~2.6 s loading screen — so the initial HTML was almost empty, hurting both SEO and perceived speed. It had to become fast and crawlable **without leaving that hosting environment**.

## What I delivered (engineering)
- **Re-architected for SSR** — the homepage and product pages render on the server, so content is in the initial HTML (good for crawlers, AI assistants and LCP).
- **`sharp` image pipeline** — backgrounds converted to WebP, everything recompressed in place.
- **Full-stack data layer** — products, resources and contacts in **MySQL via Sequelize**, exposed through Next.js route handlers, all from one consolidated service (no separate backend).
- **Authenticated admin** with protected routes.
- **Hardening** — authentication, per-IP rate limiting, security headers and input sanitisation, validated by an automated security check.
- **SEO / GEO** — JSON-LD structured data (Organization, WebSite, Product, Breadcrumb), a dynamic sitemap with per-product URLs, Open Graph images, and an `llms.txt` summary so AI assistants can cite the brand.

## Results
| Metric (mobile, production) | Before | After |
|---|---:|---:|
| Largest Contentful Paint | ~17.2 s | **~2.9 s** |
| Total Blocking Time | 3190 ms | **0 ms** |
| Page weight | 4.4 MB | **~0.5 MB** |

Product detail pages (no splash) render even faster (~2.1 s LCP).

---

<sub>Code is proprietary to Nutriline Corp; this repository documents my work for portfolio purposes. Built by <a href="https://github.com/johnvergel-dev">John Vergel</a>.</sub>