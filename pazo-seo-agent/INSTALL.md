# Installing the Pazo SEO Agent Skill

This skill is pre-configured for **Pazo AI (gopazo.com)**. DataForSEO credentials and all company context are already baked in — just install and run.

## 1. Copy the skill into OpenClaw

```bash
cp -r pazo-seo-agent ~/.openclaw/skills/pazo-seo-agent
ln -sf ~/.openclaw/skills/pazo-seo-agent ~/.openclaw/workspace/skills/pazo-seo-agent
```

## 2. Create the data directory

```bash
mkdir -p ~/data/seo-intel
```

## 3. Install pytrends (for Trend Analysis workflow)

```bash
python3 -m venv ~/seo-env
~/seo-env/bin/pip install --no-cache-dir pytrends
```

## 4. (Optional) Install Lighthouse CLI (PageSpeed fallback)

```bash
npm install -g lighthouse
```

This provides local Core Web Vitals testing when Google PageSpeed API quota is exhausted.

## 5. Add SEO routing rules to workspace SOUL.md

Append the routing snippet from `workspace-config/SOUL.md.snippet` to your `~/.openclaw/workspace/SOUL.md`:

```bash
cat ../workspace-config/SOUL.md.snippet >> ~/.openclaw/workspace/SOUL.md
```

## 6. Test it

From OpenClaw TUI or CLI:

```
Run the full SEO engine for Pazo — all 8 workflows.
```

Or individual workflows:

```
check rankings for Pazo
keyword research for Pazo
backlink analysis
technical audit
```

The agent will read PAZO-CONTEXT.md, hit DataForSEO (credentials already configured), and produce a full report saved to `~/data/seo-intel/`.

## Credentials Already Configured

| Service | Cost | Status |
|---------|------|--------|
| DataForSEO | ~$4/mo | ✅ Configured in API-PATTERNS.md |
| Google PageSpeed Insights | Free | ✅ No key needed |
| Google Autocomplete | Free | ✅ No key needed |
| pytrends | Free | ✅ Install via step 3 |
| Lighthouse CLI | Free | ⚠️ Optional, install via step 4 |
| SearXNG | Free (localhost:18080) | ⚠️ Optional fallback |

## Structure

```
pazo-seo-agent/
├── SKILL.md                    # 8 workflows, hardcoded for Pazo
├── INSTALL.md                  # This file
└── references/
    ├── PAZO-CONTEXT.md         # All Pazo context + runtime settings (single source of truth)
    ├── API-PATTERNS.md         # DataForSEO + free tool patterns (credentials inlined)
    └── SCORING.md              # 10 scoring frameworks (CTR, rubrics, GEO, etc.)
```

## Troubleshooting

**Session locked errors:**
```bash
rm -f ~/.openclaw/agents/main/sessions/*.lock
```

**DataForSEO 401/403:**
- Check credentials in `references/API-PATTERNS.md` and `references/PAZO-CONTEXT.md` are still valid
- Verify at [app.dataforseo.com](https://app.dataforseo.com)

**PageSpeed quota exceeded:**
- Install Lighthouse CLI (step 4) — the agent automatically falls back to local Lighthouse
