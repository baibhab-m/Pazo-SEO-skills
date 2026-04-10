# Pazo-SEO-skills

A dedicated SEO intelligence agent for **Pazo AI (gopazo.com)** — an AI-powered visual merchandising and retail execution platform. Built as an OpenClaw skill.

This agent handles 8 workflows for Pazo: competitive ranking analysis, keyword research, backlink intelligence, SERP & content gap analysis, technical audits, trend analysis, keyword cannibalization detection, and GEO/AI citation audits. **Everything is hardcoded for Pazo — no configuration needed.**

---

## What's in This Repo

```
Pazo-SEO-skills/
├── README.md                                    # This file
├── pazo-seo-agent/                              # The Pazo SEO skill
│   ├── SKILL.md                                 # 8 workflows, hardcoded for gopazo.com
│   ├── INSTALL.md                               # Setup instructions
│   └── references/
│       ├── PAZO-CONTEXT.md                      # Single source of truth: company, competitors, keywords, credentials
│       ├── API-PATTERNS.md                      # DataForSEO + free tool patterns (credentials inlined)
│       └── SCORING.md                           # 10 scoring frameworks (CTR curves, audit rubrics, GEO readiness)
├── data/
│   └── seo-intel/                               # Sample outputs from a real engine run (2026-04-09)
│       ├── master-report-2026-04-09.md          # Human-readable full report
│       ├── rankings-2026-04-09.jsonl            # WF1 — ranking snapshots
│       ├── keywords-2026-04-09.json             # WF2 — keyword research
│       ├── content-calendar-2026-04-09.json     # WF2 — publishing roadmap
│       ├── backlinks-2026-04-09.json            # WF3 — backlink profile
│       ├── serp-analysis-2026-04-09.json        # WF4 — SERP composition
│       ├── audit-2026-04-09.json                # WF5 — technical audit + Lighthouse
│       ├── trends-2026-04-09.json               # WF6 — Google Trends data
│       ├── cannibalization-2026-04-09.json      # WF7 — internal keyword conflicts
│       ├── geo-audit-2026-04-09.json            # WF8 — AI citation readiness
│       ├── autocomplete-2026-04-09.json         # Aggregated autocomplete mining
│       └── tracked-keywords.json                # Living keyword list (grows over time)
└── workspace-config/
    └── SOUL.md.snippet                          # Routing rules to append to your workspace SOUL.md
```

---

## Quick Setup (Clone-and-Run)

> Assumes you have OpenClaw running with a `main` agent and a workspace at `~/.openclaw/workspace/`.

```bash
# 1. Clone the repo
git clone git@github.com:baibhab-m/Pazo-SEO-skills.git
cd Pazo-SEO-skills

# 2. Install the skill into OpenClaw
mkdir -p ~/.openclaw/skills/ ~/.openclaw/workspace/skills/
cp -r pazo-seo-agent ~/.openclaw/skills/pazo-seo-agent
ln -sf ~/.openclaw/skills/pazo-seo-agent ~/.openclaw/workspace/skills/pazo-seo-agent

# 3. Set up the data directory
mkdir -p ~/data/seo-intel/
# Optional: copy the sample outputs to start with historical data
cp data/seo-intel/* ~/data/seo-intel/

# 4. Install pytrends (for the Trend Analysis workflow)
python3 -m venv ~/seo-env
~/seo-env/bin/pip install --no-cache-dir pytrends

# 5. (Optional) Install Lighthouse CLI for PageSpeed fallback
npm install -g lighthouse

# 6. Add SEO routing rules to workspace SOUL.md
cat workspace-config/SOUL.md.snippet >> ~/.openclaw/workspace/SOUL.md

# 7. Test it — from OpenClaw TUI
# Type: "Run the full SEO engine for Pazo — all 8 workflows"
```

That's it. The agent will read PAZO-CONTEXT.md, hit DataForSEO using the pre-configured credentials, and produce a full report for gopazo.com.

---

## Credentials Already Configured

This repo ships with DataForSEO credentials and all Pazo context baked in. **No additional setup needed for the basic workflows.**

| Service | Cost | Status |
|---------|------|--------|
| DataForSEO | ~$4/mo (from existing $50 deposit) | ✅ Configured in API-PATTERNS.md |
| Google PageSpeed Insights | Free | ✅ No key needed |
| Google Autocomplete | Free | ✅ No key needed |
| pytrends | Free | ✅ Install via step 4 |
| Lighthouse CLI | Free | ⚠️ Optional, step 5 |
| SearXNG | Free (localhost:18080) | ⚠️ Optional fallback |

---

## The 8 Workflows

| # | Workflow | Trigger Phrases | Output |
|---|----------|----------------|--------|
| **WF1** | Competitive Ranking Scan | "check rankings", "ranking report", "daily scan" | `rankings-YYYY-MM-DD.jsonl` |
| **WF2** | Keyword Research | "keyword research", "find keywords", "search volume" | `keywords-YYYY-MM-DD.json` + `content-calendar-*` |
| **WF3** | Backlink Analysis | "backlinks", "link gap", "referring domains" | `backlinks-YYYY-MM-DD.json` |
| **WF4** | SERP & Content Gap | "SERP analysis", "content gaps", "what are we missing" | `serp-analysis-YYYY-MM-DD.json` |
| **WF5** | Technical Audit | "page speed", "audit", "schema markup" | `audit-YYYY-MM-DD.json` |
| **WF6** | Trend Analysis | "trending", "google trends" | `trends-YYYY-MM-DD.json` |
| **WF7** | Cannibalization Detection | "cannibalization", "pages competing" | `cannibalization-YYYY-MM-DD.json` |
| **WF8** | GEO/AI Citation Audit | "AI citation", "GEO audit", "AI visibility" | `geo-audit-YYYY-MM-DD.json` |

Full details for each workflow are in `pazo-seo-agent/SKILL.md`. At the end of a full run, the agent produces `master-report-YYYY-MM-DD.md` summarizing all 8 workflows with priority actions.

---

## Pazo Context (at a glance)

Everything in `pazo-seo-agent/references/PAZO-CONTEXT.md`:

- **Company:** Gopazo (brand: Pazo AI) — AI-powered visual merchandising and retail execution platform
- **Industry:** Retail Technology / Frontline Workforce Management / Visual Merchandising SaaS
- **Stage:** Post-Seed (Techstars Bangalore)
- **Key metrics:** 380+ clients, 1.7M+ checklists/month, 27K+ active users
- **Top competitors:** Yoobic (HIGH), Zenput (HIGH), Repsly, SimplyDepo, Axonify, Bindy, GoAudits, SafetyCulture, Movista, Flagship, iwd.io, Planohero, ShelfLogic
- **Primary target audience:** Retail operations leaders, VM managers, franchise operations heads at chains with 50-500+ stores
- **Brand voice:** Professional but accessible, peace-of-mind framing, avoid "seamless/best-in-class/robust/cutting-edge"

## Key Architecture Rules (read the ABSOLUTE RULES section of SKILL.md)

1. **NO SCRIPT GENERATION** — the agent must use built-in tools (bash, web_fetch, browser), never write `.py` or `.sh` files
2. **RELEVANCE FILTERING** — every keyword must pass a 3-test rule against Pazo's industry — no broad-match noise like "fashion merchandising degree programs"
3. **DATA INTEGRITY** — structured JSON files and the master report must agree, never contradict
4. **FILE NAMING CONVENTION** — strict pattern `{type}-YYYY-MM-DD.{ext}`, one file per data type per run, no intermediate dumps

---

## Sample Output (from the 2026-04-09 run)

The `data/seo-intel/` directory contains a complete real output for Pazo AI:

- **26 keywords scanned** — 7 on Page 1, 2 in Top 3, 1 at #1, 15 AI Overviews detected
- **164 relevant keywords discovered** via autocomplete + question mining + competitor gap analysis
- **Backlinks:** 1,107 total / 479 referring domains (Domain Rank 197) vs Zenput at 11,639 (10.5x more)
- **Lighthouse:** Performance score 37/100, LCP 21,160ms (**CRITICAL — likely destroying rankings**)
- **GEO audit:** 6/12 keywords have AI Overviews, Pazo cited in 6 of them, avg citation readiness 38/100
- **Cannibalization:** 0 conflicts detected
- **Master report:** `data/seo-intel/master-report-2026-04-09.md` has the full analysis + priority actions

### Top Priority Actions (from that run)

1. **🔴 Create "planogram software" page** — Pazo's POG compliance is a differentiator but invisible (720/mo, ScorpionPlanogram owns the SERP)
2. **🔴 Publish "Yoobic vs Zenput vs Pazo" comparison page** — capture in-market switchers
3. **🔴 Fix LCP (21 seconds)** — image compression + CDN urgent
4. **🟡 Fix homepage H1 tag** — Lighthouse flagged 0 H1s
5. **🟡 Add FAQPage schema to blog posts** — boost GEO citation readiness
6. **🟢 Build backlinks** from retail/hospitality trade publications, Techstars PR

---

## Troubleshooting

**Session locked errors when running the agent:**
```bash
rm -f ~/.openclaw/agents/main/sessions/*.lock
```

**DataForSEO 401/403:**
- Credentials in `pazo-seo-agent/references/API-PATTERNS.md` expired — verify at [app.dataforseo.com](https://app.dataforseo.com)

**PageSpeed quota exceeded:**
- Install Lighthouse CLI (setup step 5) — the agent will fall back to local Lighthouse automatically

**"frontline plus for dogs" or other irrelevant keywords:**
- The relevance filter in WF2 Phase 2B should have caught these — if not, update `references/PAZO-CONTEXT.md` with more specific industry terms, or adjust the false-positive list in SKILL.md

---

## Files NOT in This Repo

- `~/seo-env/` — Python virtualenv for pytrends (recreate via setup step 4)
- `~/.openclaw/agents/main/sessions/` — agent session state (regenerated automatically)
- The OpenClaw runtime itself

---

Built on the OpenClaw platform. SKILL.md uses the standard OpenClaw skill format — markdown only, no scripts, all logic in the agent's built-in tools (bash, web_fetch, browser).
