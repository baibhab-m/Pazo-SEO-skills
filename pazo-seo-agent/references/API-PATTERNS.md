# API Patterns Reference — Pazo AI

> All credentials, the target domain (`gopazo.com`), and location/language (`2840`/`en`) are inlined below.
> Runtime substitutions: `{KEYWORD}` (for SERP/volume lookups), `{SEED}` (keyword discovery), `{URL}` (PageSpeed/web_fetch), `{QUERY}` (SearXNG), `{SHEET_ID}` + `{TAB}` (Google Sheets output).
> Company context: `references/PAZO-CONTEXT.md`.

---

## DataForSEO Endpoints

**Base URL:** `https://api.dataforseo.com`
**Auth:** HTTP Basic with `baibhab@saasden.club:3a26587c314d0f77`
**Cost:** ~$4/mo total. $50 deposit lasts ~12 months.

### 1. SERP API — Google Rankings ($0.002/call)

```bash
curl -s -X POST -u "baibhab@saasden.club:3a26587c314d0f77" \
  -H "Content-Type: application/json" \
  "https://api.dataforseo.com/v3/serp/google/organic/live/regular" \
  -d '[{"keyword": "{KEYWORD}", "location_code": 2840, "language_code": "en", "depth": 20}]'
```

**Response parsing:**
- Organic results: `tasks[0].result[0].items[]` → `rank_absolute`, `url`, `domain`, `title`, `description`
- SERP features: `tasks[0].result[0].item_types[]` → `featured_snippet`, `people_also_ask`, `ai_overview`
- AI Overview details: look for items with `type: "ai_overview"` — extract cited sources

### 2. Search Volume — Keyword Metrics ($0.05/batch, up to 700 keywords)

```bash
curl -s -X POST -u "baibhab@saasden.club:3a26587c314d0f77" \
  -H "Content-Type: application/json" \
  "https://api.dataforseo.com/v3/keywords_data/google_ads/search_volume/live" \
  -d '[{"keywords": ["{KW1}","{KW2}","{KW3}"], "location_code": 2840, "language_code": "en"}]'
```

**Response:** `tasks[0].result[]` → `keyword`, `search_volume`, `competition_index` (0-100), `cpc`

### 3. Keyword Suggestions ($0.075/call)

```bash
curl -s -X POST -u "baibhab@saasden.club:3a26587c314d0f77" \
  -H "Content-Type: application/json" \
  "https://api.dataforseo.com/v3/dataforseo_labs/google/keyword_suggestions/live" \
  -d '[{"keyword": "{SEED}", "location_code": 2840, "language_code": "en", "limit": 50}]'
```

**Response:** `tasks[0].result[0].items[]` → `keyword`, `keyword_info.search_volume`, `keyword_properties.keyword_difficulty`

### 4. Ranked Keywords — What a Domain Ranks For ($0.05/call)

```bash
curl -s -X POST -u "baibhab@saasden.club:3a26587c314d0f77" \
  -H "Content-Type: application/json" \
  "https://api.dataforseo.com/v3/dataforseo_labs/google/ranked_keywords/live" \
  -d '[{"target": "gopazo.com", "location_code": 2840, "language_code": "en", "limit": 100}]'
```

**Response:** `tasks[0].result[0].items[]` → `keyword_data.keyword`, `keyword_data.keyword_info.search_volume`, `ranked_serp_element.serp_item.rank_absolute`, `ranked_serp_element.serp_item.url`

### 5. Competitors Domain ($0.05/call)

```bash
curl -s -X POST -u "baibhab@saasden.club:3a26587c314d0f77" \
  -H "Content-Type: application/json" \
  "https://api.dataforseo.com/v3/dataforseo_labs/google/competitors_domain/live" \
  -d '[{"target": "gopazo.com", "location_code": 2840, "language_code": "en", "limit": 20}]'
```

**Response:** `tasks[0].result[0].items[]` → `domain`, `avg_position`, `se_keywords`, `intersections`

### 6. Backlinks Summary ($0.02/call)

```bash
curl -s -X POST -u "baibhab@saasden.club:3a26587c314d0f77" \
  -H "Content-Type: application/json" \
  "https://api.dataforseo.com/v3/backlinks/summary/live" \
  -d '[{"target": "gopazo.com"}]'
```

**Response:** `tasks[0].result[0]` → `backlinks`, `referring_domains`, `rank` (0-1000)

### 7. Backlinks Detail ($0.02/call)

```bash
curl -s -X POST -u "baibhab@saasden.club:3a26587c314d0f77" \
  -H "Content-Type: application/json" \
  "https://api.dataforseo.com/v3/backlinks/backlinks/live" \
  -d '[{"target": "gopazo.com", "limit": 100, "order_by": ["rank,desc"]}]'
```

**Response:** `tasks[0].result[0].items[]` → `url_from`, `domain_from`, `anchor`, `dofollow`, `rank`

### 8. Referring Domains ($0.02/call)

```bash
curl -s -X POST -u "baibhab@saasden.club:3a26587c314d0f77" \
  -H "Content-Type: application/json" \
  "https://api.dataforseo.com/v3/backlinks/referring_domains/live" \
  -d '[{"target": "gopazo.com", "limit": 100, "order_by": ["rank,desc"]}]'
```

**Response:** `tasks[0].result[0].items[]` → `domain`, `rank`, `backlinks`, `first_seen`

---

## Free Tools (supplement DataForSEO)

### Google Autocomplete — Keyword Discovery (no key needed)

```
web_fetch: https://suggestqueries.google.com/complete/search?client=firefox&q={KEYWORD}&hl=en&gl=us
```

Response is a JSON array: `[query, [suggestion1, suggestion2, ...]]`

**Deep mining:** Append each letter a-z to the seed and query. Example: `{KEYWORD} a`, `{KEYWORD} b`, ... `{KEYWORD} z`.
**Question mining:** Prepend: how, what, why, when, where, which, who, can, does, is.

### PageSpeed Insights — Core Web Vitals (free, daily quota)

```
web_fetch: https://www.googleapis.com/pagespeedonline/v5/runPagespeed?url={URL}&strategy=mobile
web_fetch: https://www.googleapis.com/pagespeedonline/v5/runPagespeed?url={URL}&strategy=desktop
```

Key metrics in response:
- `lighthouseResult.categories.performance.score` (0-1, multiply by 100)
- `lighthouseResult.audits['largest-contentful-paint']`
- `lighthouseResult.audits['cumulative-layout-shift']`
- `lighthouseResult.audits['interactive']`

### pytrends — Google Trends (via Python virtualenv)

```bash
~/seo-env/bin/python3 -c "
from pytrends.request import TrendReq
import json
pytrends = TrendReq(hl='en-US', tz=360)
pytrends.build_payload(['{KW1}','{KW2}'], timeframe='today 12-m')
df = pytrends.interest_over_time()
print(df.to_json())
"
```

Do NOT use `python3` directly — it won't find pytrends. Always use `~/seo-env/bin/python3`.

### SearXNG — Local Search Fallback

```bash
curl -s "http://localhost:18080/search?q={QUERY}&format=json&engines=google,bing,duckduckgo"
```

### Lighthouse CLI — Local PageSpeed Fallback (when Google API quota exhausted)

```bash
npx lighthouse {URL} --output json --quiet --chrome-flags="--headless --no-sandbox" 2>/dev/null
```

Key metrics in output:
- `categories.performance.score` (0-1, multiply by 100)
- `audits['largest-contentful-paint'].numericValue` (ms)
- `audits['cumulative-layout-shift'].numericValue`
- `audits['total-blocking-time'].numericValue` (ms)

If `npx` is not available, try: `node_modules/.bin/lighthouse` or note "Lighthouse not installed".

### Google Rich Results Test (manual validation)

URL: `https://search.google.com/test/rich-results?url={URL}`

---

## DataForSEO Additional Endpoints

### 9. Domain Intersection — Link Gap Analysis ($0.05/call)

Find domains that link to competitors but NOT to the target domain. Use in WF3 Phase 6.

```bash
curl -s -X POST -u "baibhab@saasden.club:3a26587c314d0f77" \
  -H "Content-Type: application/json" \
  "https://api.dataforseo.com/v3/backlinks/domain_intersection/live" \
  -d '[{"targets": {
    "1": "{COMPETITOR1}",
    "2": "{COMPETITOR2}",
    "3": "{COMPETITOR3}"
  }, "exclude_targets": ["gopazo.com"], "limit": 100, "order_by": ["rank,desc"]}]'
```

**Response:** `tasks[0].result[0].items[]` → domains linking to competitors but NOT to target. Each item has `domain`, `rank`, `backlinks`.

### 10. Content Analysis — Search by keyword ($0.002/call)

Find pages discussing a topic with sentiment and social metrics. Use for GEO audit and competitor content analysis.

```bash
curl -s -X POST -u "baibhab@saasden.club:3a26587c314d0f77" \
  -H "Content-Type: application/json" \
  "https://api.dataforseo.com/v3/content_analysis/search/live" \
  -d '[{"keyword": "{KEYWORD}", "limit": 20, "order_by": ["rank,desc"]}]'
```

**Response:** `tasks[0].result[0].items[]` → `url`, `domain`, `title`, `content_info.sentiment`, `social_metrics`

---

## Google Sheets Output (via gws CLI)

Use the `gws` CLI to write SEO data to Google Sheets. The Sheet ID is in CONFIG.md (`sheet_id` field).

### Create a new Sheet

```bash
export PATH="$HOME/.nvm/versions/node/v22.22.1/bin:$PATH"
gws drive files create --json '{"name": "SEO Report - Pazo AI", "mimeType": "application/vnd.google-apps.spreadsheet"}'
```

Response includes `"id"` — save this as the sheet_id in CONFIG.md.

### Add tabs

```bash
gws sheets spreadsheets batchUpdate --params '{"spreadsheetId": "{SHEET_ID}"}' --json '{
  "requests": [
    {"updateSheetProperties": {"properties": {"sheetId": 0, "title": "Summary"}, "fields": "title"}},
    {"addSheet": {"properties": {"title": "Rankings"}}},
    {"addSheet": {"properties": {"title": "Keywords"}}},
    {"addSheet": {"properties": {"title": "Backlinks"}}},
    {"addSheet": {"properties": {"title": "SERP Gaps"}}},
    {"addSheet": {"properties": {"title": "Technical"}}},
    {"addSheet": {"properties": {"title": "Trends"}}},
    {"addSheet": {"properties": {"title": "Cannibalization"}}},
    {"addSheet": {"properties": {"title": "GEO Audit"}}}
  ]
}'
```

### Write data to a tab

Build row arrays in Python, then write:

```bash
gws sheets spreadsheets values update \
  --params '{"spreadsheetId":"{SHEET_ID}","range":"{TAB}!A1","valueInputOption":"RAW"}' \
  --json '{"values": [["Header1","Header2"],["row1col1","row1col2"]]}'
```

**Pattern:** Build the values array using inline `python3 -c "..."` that reads from the saved JSON files in `~/data/seo-intel/`, transforms to row arrays, and outputs JSON. Pipe to a temp file, then pass to gws.

### Make Sheet publicly viewable

```bash
gws drive permissions create --params '{"fileId": "{SHEET_ID}"}' --json '{"role": "reader", "type": "anyone"}'
```
