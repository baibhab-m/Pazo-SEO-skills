# Scoring Frameworks Reference

> All scoring systems used across SEO workflows. Referenced by SKILL.md — do not duplicate these inline.

---

## 1. CTR Curve (Google Organic CTR by Position)

| Position | CTR |
|----------|-----|
| 1 | 28.5% |
| 2 | 15.7% |
| 3 | 11.0% |
| 4 | 8.0% |
| 5 | 7.2% |
| 6 | 5.1% |
| 7 | 4.0% |
| 8 | 3.2% |
| 9 | 2.8% |
| 10 | 2.5% |
| 11-20 | 1.0% |
| Not ranked | 0% |

---

## 2. Traffic Value Formulas

- `estimated_traffic = search_volume x CTR_for_position`
- `traffic_value = estimated_traffic x CPC` (use default CPC from CONFIG.md if CPC unavailable)
- `traffic_potential = search_volume x 28.5%` (what you'd get at position #1)
- `traffic_gap = traffic_potential - estimated_traffic` (what you're leaving on the table)
- `SOV = domain_traffic / total_traffic x 100%` (share of voice across all tracked keywords)

---

## 3. Keyword Opportunity Scoring (6-Dimension Framework)

**Primary formula:** `Opportunity = (Volume x Intent Value) / Difficulty`

**Intent weights:** Informational=1, Navigational=1, Commercial=2, Transactional=3

**Six scoring dimensions:**
1. **Conversion Potential:** Direct business actions (signups, demos) vs awareness-building
2. **Search Volume:** Higher = greater reach. Zero-volume keywords still matter if first-party signals confirm demand
3. **Click Potential:** Likelihood of actual clicks vs zero-click AI answers. Long-tail (7+ words) yield 2.3x higher satisfaction
4. **Real-World Demand Signals:** Frequency in sales calls, GitHub issues, Reddit threads, support tickets
5. **Trend Direction:** Prioritize stable/growing trends; avoid declining keywords unless first-party signals confirm sustained demand
6. **Attainability:** Keyword difficulty 0-49% for new content; established pages can pursue higher difficulty

---

## 4. Keyword Difficulty Thresholds

| Range | Label | Strategy |
|-------|-------|----------|
| 0-29% | Easy | Target immediately, especially new content |
| 30-49% | Moderate | Target with strong content + some backlinks |
| 50-69% | Hard | Need significant authority + backlinks |
| 70-100% | Very Hard | Long-term play, sustained campaign required |

---

## 5. On-Page Audit Rubric (15 Factors, 150 Points Total)

Score each factor 0-10. Overall Score = sum / 150 x 100.

### Title Tag (10 pts)
- Exists: +2
- Length 50-60 chars: +3
- Contains primary keyword: +3
- Unique across site: +2

### Meta Description (10 pts)
- Exists: +2
- Length 105-160 chars: +3
- Contains keyword: +2
- Active voice + action-oriented: +3

### H1 Tag (10 pts)
- Exactly one H1: +4
- Contains primary keyword: +3
- Under 60 chars: +3

### Heading Hierarchy (10 pts)
- Proper nesting (H1 > H2 > H3): +4
- Descriptive headings (not "Section 1"): +3
- Headings answered immediately in first sentence: +3

### Keyword Usage (10 pts)
- In first 100 words: +3
- Natural distribution: +4
- No stuffing: +3

### Content Quality (10 pts)
- Length appropriate for intent (2000+ for guides): +3
- Short paragraphs (2-4 sentences): +2
- Lists/tables used: +2
- Multimedia present: +3

### Internal Links (10 pts)
- 3+ internal links: +4
- Descriptive anchor text: +3
- Links to relevant pages: +3

### External Links (10 pts)
- Cites authoritative sources: +5
- Links to original data/research: +3
- No broken external links: +2

### Image Optimization (10 pts)
- Alt text present on all images: +4
- Alt text descriptive (not "image1.png"): +3
- Alt text under 125 chars: +1
- Optimized file sizes: +2

### URL Structure (10 pts)
- Contains keyword: +3
- 3-5 words, hyphens: +3
- No dates, parameters, random numbers: +2
- Lowercase: +2

### Schema Markup (10 pts)
- JSON-LD present: +4
- Correct type for page: +3
- Validates in Rich Results Test: +3

### Canonical Tag (10 pts)
- Present: +5
- Points to correct URL: +5

### Open Graph Tags (10 pts)
- og:title, og:description, og:image present: +7
- Twitter card tags: +3

### Mobile Viewport (10 pts)
- Viewport meta tag: +5
- Responsive design: +5

### HTTPS & Security (10 pts)
- HTTPS: +5
- No mixed content: +3
- Security headers: +2

---

## 6. GEO Citation Readiness Score (AI Visibility)

Score content for likelihood of being cited by AI systems (ChatGPT, Perplexity, Google AI Overviews, Claude).

| Factor | Points | What to Check |
|--------|--------|---------------|
| Clear definition paragraph | 0-20 | 40-60 word definition near the top of the page, direct answer to the query |
| Structured data | 0-15 | Tables, numbered lists, FAQ schema, comparison matrices |
| Authoritative citations | 0-15 | Links to research papers, official docs, primary sources |
| Expert attribution | 0-10 | Named author with credentials, organization backing |
| Statistical specificity | 0-15 | Concrete numbers, benchmarks, percentages (not vague claims) |
| Section independence | 0-10 | Each H2 section works standalone when extracted out of context |
| Fluency & readability | 0-10 | Flesch-Kincaid grade 8-10 ideal, no jargon walls, clear sentence structure |
| Entity disambiguation | 0-5 | Clear, unambiguous subject naming (restate subjects, avoid vague pronouns) |

**Total: /100 points**

| Score | Rating | Meaning |
|-------|--------|---------|
| 80-100 | Citation Ready | High probability of AI citation |
| 60-79 | Needs Work | Some structural improvements needed |
| 40-59 | Low Probability | Major gaps in citation signals |
| 0-39 | Not Optimized | Content not structured for AI consumption |

**Key research findings:**
- Statistics increase AI citation likelihood by 33.9%
- Expert quotes boost visibility by 32%
- Clear, fluent writing improves citation rates by 30%

---

## 7. Content Gap Quality Assessment Matrix

| Gap Type | Indicator | Solution |
|----------|-----------|----------|
| Recency | Competitor content >2 years old | Create fresher content with current data |
| Depth | Competitor coverage is shallow | Create comprehensive, expert-level content |
| Experience | Competitor content is theoretical | Add real benchmarks, code examples, case studies |
| Format | No good comparison/tool content | Create the format that's missing |
| Authority | Competitor has weak backlink profile | Easier to outrank with strong content + few links |

---

## 8. Cannibalization Severity Score

When 2+ URLs from the same domain rank for the same keyword:

| Severity | Criteria | Impact |
|----------|----------|--------|
| HIGH | Both URLs within 5 positions of each other in top 20 | Actively splitting clicks, confusing Google |
| MEDIUM | Both in top 50, but >5 positions apart | Diluting authority, one page underperforming |
| LOW | One URL in top 50, other much lower | Minor signal splitting, monitor |

**Weighting factors:**
- Multiply severity by search volume: high-volume cannibalization is more urgent
- Same intent = true cannibalization (must fix). Different intents = may be acceptable
- Estimated traffic loss: sum traffic of both pages vs what the stronger page would get alone

---

## 9. Backlink Health Indicators

| Metric | Healthy | Warning | Action |
|--------|---------|---------|--------|
| Dofollow ratio | 70%+ dofollow | <50% dofollow | Acquire more dofollow links |
| Anchor text distribution | <30% exact match | >30% exact match | Looks spammy, diversify anchors |
| Toxicity score | <30 | 60+ | Flag for removal/disavowal |
| Domain diversity | Broad spread across many domains | >50% from <5 domains | Diversify link sources |
| Link placement | Body links (editorial) | Sidebar/footer links | Focus outreach on editorial placements |

---

## 10. Content Lifecycle Maturity Model

| Phase | Timeline | Behavior |
|-------|----------|----------|
| Launch | Month 1 | Initial traffic spike (misleading — don't judge by this) |
| Valley of Death | Months 2-8 | 68% of articles abandoned here — DON'T give up |
| SEO Compound Effect | Month 9+ | Rankings improve, traffic multiplies |
| Productive Maturity | Months 18-24 | ROI triples compared to launch |
| Maintenance | Ongoing | Updated pages retain 60% of SEO value; neglected drop to 15% |

**Refresh rule:** Audit all content every 6 months. Update data, add new sections, refresh examples.
