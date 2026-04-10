# Pazo AI — Company Context & Settings

> **THIS FILE IS THE SINGLE SOURCE OF TRUTH FOR PAZO.**
> Every SEO workflow reads this first. All targeting, competitor analysis,
> keyword research, content recommendations, and brand voice rules come from here.

---

## Domain

- **Primary domain:** gopazo.com (also uses www.gopazo.com — redirects observed)
- **Subdomains to track:** blog.gopazo.com (implied from blog archive), app.gopazo.com (implied from login references)
- **GSC site URL:** none verified

## Company

- **Company name:** Gopazo (brand: Pazo AI / "Pazo")
- **Brand name (for reports):** Gopazo / Pazo AI
- **One-line description:** AI-powered visual merchandising and retail execution platform that replaces paper checklists with mobile-first digital task management, live photo verification, and real-time compliance alerting for frontline store and hospitality teams.
- **Industry/vertical:** Retail Technology / Frontline Workforce Management / Visual Merchandising SaaS
- **Stage:** Post-Seed (Techstars Bangalore acceleration; specific round unknown)
- **Founded:** 2015
- **HQ:** India (Bangalore implied from Techstars mention)
- **Funding:** Techstars Bangalore accelerator; specific amount undisclosed
- **Key metrics:** 380+ clients, 1.7M+ checklists created/month, 27,000+ active users, 3 co-founders

## Key Differentiators

- **AI-Agent first:** "Best in market AI-Agent" — auto-flags issues, escalates compliance gaps, routes alerts. Differentiates from checklist-only tools
- **Live image verification with geotagging:** No saved/formulaic photo uploads — real-time, location-verified proof-of-work
- **Mobile-first, frontline-simple:** "I just snap a photo and I'm done" — designed for non-desk workers
- **Planogram compliance:** Explicit POG/planogram execution tracking (rare in this category)
- **Multi-level escalation engine:** Escalates to the right person at the right level — corporate vs. store vs. franchisee

## Brand Voice

- **Tone:** Professional but accessible; emphasizes peace-of-mind ("paz" = peace in Spanish)
- **Forbidden terms:** "seamless," "best-in-class," "robust," "cutting-edge," "synergy"
- **Preferred style:** Concrete benefits over features, real user quotes, problem-first framing, metrics-backed claims

## Target Audience

- **Primary:** Retail operations leaders, visual merchandising managers, franchise operations heads at chains with 50-500+ stores
- **Secondary:** Hospitality groups (restaurants, hotels) managing frontline compliance and audit cycles
- **Pain points:** Paper-based audits consuming hours, no visibility until quarterly reviews, compliance gaps costing promotions and footfall, fragmented apps creating frontline chaos

## Competitors

Known competitors identified from website copy + DataForSEO competitor analysis. Agent should discover more dynamically from SERP data.

| Competitor | Domain | Description | Threat Level |
|-----------|--------|-------------|-------------|
| Yoobic | yoobic.com | Enterprise retail ops platform; 350+ global enterprise clients; heavy on execution workflows | HIGH |
| Zenput | zenput.com | Restaurant/convenience ops execution; strong US footprint; now part of Ecolab | HIGH |
| Repsly | repsly.com | Retail execution software, strong US footprint | MEDIUM |
| SimplyDepo | simplydepo.com | Retail execution and CPG field sales | MEDIUM |
| Axonify | axonify.com | Frontline employee training + operations | MEDIUM |
| Bindy | bindy.com | Store audit and task management | MEDIUM |
| GoAudits | goaudits.com | Store audit software | MEDIUM |
| SafetyCulture | safetyculture.com | Workplace operations, checklists, audits | MEDIUM |
| Movista | movista.com | Retail execution platform | MEDIUM |
| Flagship | flagship.ai / flagship.io | Visual merchandising | MEDIUM |
| iwd.io | iwd.io | Visual merchandising software | MEDIUM |
| Planohero | planohero.com | Planogram software | LOW |
| ShelfLogic | shelflogic.com | Planogram software | LOW |
| ScorpionPlanogram | scorpionplanogram.com | Planogram software | LOW |
| WFM (various) | various | General workforce management platforms with retail modules | MEDIUM |

Competitors API found 13,656 keyword intersections — large competitive landscape. Additional discovery via SERP analysis on every run.

## Seed Keywords

Starting keyword set across categories. The agent grows this into `~/data/seo-intel/tracked-keywords.json`.

- **Core:** visual merchandising software, retail execution software, planogram software, store audit software, retail compliance software, retail task management software, frontline workforce management
- **Head-to-Head:** gopazo vs yoobic, gopazo vs zenput, pazo vs retail execution software, alternatives to yoobic, alternatives to zenput, yoobic alternatives, zenput alternatives
- **Problem-Aware:** store checklist app, retail store audit software, how to improve store compliance, how to conduct store audit, how to manage frontline workers, paper-based audit problems, retail compliance issues
- **Brand:** gopazo, pazo app login, gopazo pricing, gopazo app, pazo AI, pazo visual merchandising, gopazo review
- **GEO:** what is visual merchandising, how does planogram software work, retail execution meaning, how to improve retail store operations, what is store audit, what is retail execution, retail compliance definition

## Business Goals (SEO-Specific)

Rank by priority:
1. **Increase organic traffic** for category keywords (visual merchandising software, retail execution software, planogram software)
2. **Capture in-market switchers** — build visibility for "vs [competitor]" comparison queries (highest conversion intent)
3. **Outrank Yoobic and Zenput** for high-volume commercial keywords
4. **Improve GEO/AI citation** — Pazo AI should appear in AI Overviews for operational excellence queries
5. **Build backlink authority** from retail/hospitality industry publications and blogs
6. **Fix technical SEO** — robots.txt is minimal (no AI crawler entries), sitemap present but needs audit, LCP at 21s is critical
7. **Capture high-intent bottom-of-funnel keywords:** "gopazo pricing", "gopazo review", "pazo alternatives"

## Pricing

Pricing page (pricing-plans) currently redirects to homepage — actual pricing not publicly visible. SaaS model implied with per-seat or per-location pricing. Agent can estimate from G2/alternative review sites or Capterra listings.

## Notes

- Blog content cluster around restaurant and hospitality operations — heavy on compliance/checklist topics (restaurant health inspection, fire risk assessment, food safety audits). Suggests two ICP tracks: (1) retail VM, (2) hospitality ops
- Website uses **Pazo AI** as the product name; company name is **Gopazo**. Both matter for brand keyword targeting
- "Alternatives to" pages exist for Yoobic, Zenput, and Wooqer — strategy of capturing competitor switchers
- Website is www.gopazo.com but canonical may point to gopazo.com — needs canonical audit
- AI crawler access: robots.txt is minimal with no explicit AI bot allowances — recommend adding GPTBot, ClaudeBot, PerplexityBot explicitly
- **LCP is 21 seconds** per Lighthouse — critical urgency, likely destroying rankings

---

## Agent Runtime Settings

These are the technical settings the agent needs to operate. DO NOT modify unless changing the environment.

### DataForSEO Credentials

- **Login:** baibhab@saasden.club
- **Password:** 3a26587c314d0f77
- **Base URL:** https://api.dataforseo.com
- **Budget:** ~$4/mo total (from a $50 deposit that lasts ~12 months)

### Location & Language

- **Location code:** 2840 (US — primary market)
- **Language code:** en

### Default CPC (for traffic value estimation)

- **Default CPC:** $5 (B2B SaaS typical: $5-15)

### Slack Channel

- **Channel ID:** (set this to enable Slack delivery of reports)

### Google Sheet Output

- **sheet_id:** (set a Google Sheet ID here, or leave blank to skip Sheet output)
