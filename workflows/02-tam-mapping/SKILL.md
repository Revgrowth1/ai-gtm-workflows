---
name: tam-map
description: Build total addressable market databases for any B2B vertical. Multi-source data collection, deduplication, enrichment hand-off. USE WHEN user says "tam-map" OR "TAM map" OR "build TAM" OR "total addressable market" OR "scrape industry" OR "map the market" OR "how many companies" OR "build a lead database" OR "industry database" OR wants to collect business data from multiple sources for a vertical.
---

# TAM MAP - Total Addressable Market Builder

Build comprehensive business databases for any B2B vertical by discovering, scraping, and deduplicating data from every available source. Produces a unified, deduplicated CSV ready for enrichment.

**Origin:** A roofing TAM build - 113K raw records from 20+ sources, deduplicated to 89,562 unique businesses, 20,557 campaign-ready leads at ~$15 total cost.

## The 7 Phases

| Phase | What Happens | Output |
|---|---|---|
| 1. Source Discovery | Research ALL data sources for the vertical | Source manifest (scored list) |
| 1.5. Keyword Expansion | Discover adjacent keywords that share the same TAM | Expanded keyword list |
| 2. Config Generation | Build TAMConfig with sources, keywords, NAICS codes | `config.json` |
| 3. Collection | Run scrapers for each source | `{source}/businesses.csv` per source |
| 4. Deduplication | 3-tier dedup: domain -> name+state -> phone | `all_sources_deduped.csv` |
| 4.5. Existing Leads Exclusion | Remove leads already in your email platform (ALWAYS run, not optional) | `net_new_leads.csv` |
| 5. Enrichment Hand-off | Feed net new CSV into enrichment pipeline | Campaign-ready leads |

---

## Phase 1: Source Discovery (THE MOST IMPORTANT PHASE)

The quality of the TAM depends on source breadth. For every vertical, research and catalog every available data source across ALL of these categories:

### Source Categories Checklist

| # | Category | What to Look For | Example Sources |
|---|---|---|---|
| 1 | **Government/regulatory** | State licenses, professional registries, regulatory filings | State contractor boards, SEC, FDA, FCC, state bar associations, Socrata open data portals |
| 2 | **Federal contracts** | Government contract recipients by NAICS | SAM.gov / USASpending.gov (free API, no auth) |
| 3 | **Industry associations** | Trade orgs, certification bodies, member directories | NRCA (roofing), PHCC (plumbing), CompTIA (IT), ABA (legal) |
| 4 | **Manufacturer/vendor directories** | Certified partner/contractor/reseller locators | GAF/Owens Corning (roofing), Kohler (plumbing), Salesforce AppExchange (SaaS) |
| 5 | **Company databases** | Structured business databases searchable by industry | IcyPeas (any vertical), Crunchbase (tech), D&B |
| 6 | **Local/maps** | Geographic business listings | Google Maps via Serper ZIP code mode |
| 7 | **Review platforms** | Industry-specific review sites | G2/Capterra (SaaS), Clutch (agencies), Thumbtack/Houzz/Porch (home services), TrustPilot |
| 8 | **Social platforms** | Business pages on social networks | Facebook pages, LinkedIn company search |
| 9 | **Business directories** | General business listings | BBB (any B2B), Chamber of Commerce, industry yellow pages |
| 10 | **Awards/rankings** | Recognition and "best of" lists | Inc 5000, Deloitte Fast 500, industry-specific awards, "Top X [vertical] companies" |
| 11 | **Job boards** | Companies actively hiring for vertical-specific roles | Indeed, LinkedIn Jobs - signals active/growing companies |
| 12 | **Events/conferences** | Exhibitor and sponsor directories | Trade show exhibitor lists, conference sponsor pages |
| 13 | **Investor/funding** | Funded companies in the vertical | Crunchbase, PitchBook, AngelList (for tech/SaaS verticals) |
| 14 | **Open data** | Government statistics with company lists | Census Business Patterns, BLS, state open data portals |
| 15 | **Marketplace/aggregator** | Platform-specific directories | HomeAdvisor (home services), Upwork (agencies), AWS Marketplace (SaaS) |
| 16 | **Academic/research** | Industry reports with company lists | Gartner quadrants, Forrester waves, industry census reports |

### How to Research Sources

1. **Web search** for `"{vertical}" site:*.gov database` to find government/regulatory sources
2. **Web search** for `"{vertical}" association directory members` to find trade associations
3. **Web search** for `"{vertical}" certified contractors` or `"{vertical}" partner directory` for manufacturer/vendor directories
4. **Check NAICS codes** at https://www.naics.com/search/ - needed for SAM.gov
5. **Check state licensing** - search `"{vertical}" license {state}` for each major state
6. **Check review platforms** - which platforms does this vertical use? (G2 for SaaS, Houzz for home services, Clutch for agencies)
7. **Check if IcyPeas has coverage** - run a free count query first

### Source Manifest Output

Create `manifest.json` in the output directory:

```json
{
  "vertical": "plumbing",
  "date": "2026-03-22",
  "total_sources": 18,
  "sources": [
    {
      "name": "icypeas_plumbing",
      "category": "company_database",
      "method": "api",
      "url": "https://app.icypeas.com",
      "estimated_records": 30000,
      "has_owner_names": false,
      "has_emails": false,
      "has_addresses": false,
      "has_phone": false,
      "cost_estimate": "IcyPeas credits",
      "priority": 1,
      "notes": "Broad coverage, domains + LinkedIn URLs"
    }
  ],
  "total_estimated_records": 95000,
  "estimated_unique_after_dedup": 45000
}
```

### Priority Scoring

- **Priority 1 (must-have):** Sources with owner names baked in (state licenses), broad coverage databases (IcyPeas), Google Maps
- **Priority 2 (high value):** Industry association directories, manufacturer certs, BBB, SAM.gov
- **Priority 3 (nice to have):** Review platforms, Facebook pages, awards lists, job board signals

---

## Phase 1.5: Keyword Expansion

Before configuring sources, discover adjacent keywords that target the same TAM. The primary keyword alone often misses 30-60% of the market.

### How It Works

1. **Start with the primary keyword** (e.g., "coffee shop")
2. **Brainstorm adjacent terms** that describe the same businesses differently:
   - Synonyms: "cafe", "coffeehouse"
   - Subtypes: "espresso bar", "coffee roaster", "coffee stand"
   - Related: "bakery cafe", "tea and coffee"
3. **Run IcyPeas free count queries** for each candidate keyword to estimate incremental volume
4. **Check overlap** - many adjacent keywords return 40-70% duplicates. That's fine - dedup handles it. The goal is to catch the 30-60% that only appear under one keyword.

### Example: Coffee Shop Expansion

| Keyword | IcyPeas Count | Incremental After Dedup |
|---|---|---|
| coffee shop | 22,000 | 22,000 (base) |
| cafe | 43,000 | ~9,855 net new |
| coffee roaster | 9,000 | ~1,703 net new |
| espresso bar | 16,000 | ~2,109 net new |
| **Total** | 90,000 raw | **~35,667 unique** |

### Rules

- **Always run counts before pulling** - IcyPeas count queries are free. Don't pull 43K "cafe" records if count shows only 2K.
- **Dedup cross-keyword overlap** - use the same dedup pipeline. Adjacent keywords may overlap 40-70%.
- **Run expanded keywords through ZIP scrape too** - Google Maps queries for "cafe near [ZIP]" find different businesses than "coffee shop near [ZIP]".
- **Document the expansion** - save the keyword -> count -> incremental mapping in the manifest for future builds.

---

## Phase 2: Config Generation

Build a TAMConfig JSON from the manifest. Example config structure:

```python
config = TAMConfig(
    vertical_name="plumbing",
    keywords=["plumbing", "plumber", "plumbing contractor", "plumbing company", "plumbing repair"],
    naics_codes=["238220"],
    sources=[
        TAMSource(
            name="icypeas_plumbing",
            category="company_database",
            method="api",
            config={"type": "icypeas"},
            estimated_records=30000,
            priority=1,
        ),
        TAMSource(
            name="sam_gov_plumbing",
            category="federal_contracts",
            method="api",
            config={"type": "sam_gov"},
            estimated_records=2000,
            priority=2,
        ),
        # ... more sources
    ],
    generic_filters=["plumbing contractor", "best plumber", "plumber near me"],
    output_dir="./output/plumbing_20260322",
)
config.save("config.json")
```

### NAICS Code Reference (Common Verticals)

| Vertical | NAICS | Description |
|---|---|---|
| Roofing | 238160 | Roofing Contractors |
| Plumbing | 238220 | Plumbing, Heating, AC Contractors |
| Electrical | 238210 | Electrical Contractors |
| HVAC | 238220 | (same as Plumbing) |
| Landscaping | 561730 | Landscaping Services |
| Pest Control | 561710 | Exterminating and Pest Control |
| Painting | 238320 | Painting and Wall Covering |
| General Construction | 236220 | Commercial Building Construction |
| IT Services | 541512 | Computer Systems Design |
| Marketing Agencies | 541810 | Advertising Agencies |
| Management Consulting | 541611 | Administrative Management Consulting |
| SaaS | 511210 | Software Publishers |
| Accounting | 541211 | Offices of CPAs |
| Legal | 541110 | Offices of Lawyers |

---

## Phase 3: Collection

### Automated Sources

These source types can be automated with reusable scraper modules:

| Source Type | Method | Notes |
|---|---|---|
| IcyPeas | API | Broad company database, domains + LinkedIn URLs |
| SAM.gov | API | Free federal contracts data by NAICS |
| Serper site-scoped | Web search | Any website with a directory (BBB, Houzz, etc.) |

### Google Maps (via ZIP Code Scraping)

For local/service businesses, run Google Maps scraping via Serper's local search:

**Methodology:**
1. Load a comprehensive US ZIP code list (~40K ZIPs)
2. For each ZIP, query `"{keyword}" near {ZIP}` via Serper local results
3. Extract business name, address, phone, website, rating
4. Output to `businesses.csv` with the unified schema

### Bespoke Sources (Write Per-Vertical)

For sources without a reusable scraper (state license DBs, niche directories), write a one-off script. Follow these patterns:

**Serper site-scoped scrape** (for any website with a directory):
```python
# Pseudocode for site-scoped scraping
# 1. Define query templates: site:{site} inurl:profile "{keyword}" "{state}"
# 2. For each state + keyword combo, run Serper query
# 3. Extract business name, state, source URL from results
# 4. Filter: only keep profile pages (check URL pattern)
# 5. Output to businesses.csv with unified schema
```

**State license database** (requires per-state research):
- Check if state has an open data portal (Socrata)
- Check if state has a searchable license lookup
- Some states expose CSV/API (FL DBPR, CA CSLB, IL Socrata)
- Some require Selenium (CAPTCHAs, JS SPAs)
- Owner names from license records are the highest-value free data

**Every bespoke scraper MUST output `businesses.csv` with the unified schema columns.**

---

## Phase 4: Deduplication

The dedup engine auto-detects CSV column names and maps them to the unified schema. No hardcoded source mappers needed.

### Three-Tier Dedup Algorithm

1. **Tier 1: Domain match** - Records with the same normalized domain are merged. Keeps the record with the most populated fields, fills empty fields from duplicates.
2. **Tier 2: Company name + state** - Domainless records matched to domain records by normalized company name + exact state.
3. **Tier 3: Phone match** - Remaining unmatched records matched by normalized 10-digit phone number.
4. **Internal dedup** - Remaining unmatched records deduplicated among themselves by name+state.

### Output

- `all_sources_deduped.csv` - unified deduplicated master list
- `dedup_stats.json` - per-source counts, overlap analysis, dedup rates

---

## Phase 4.5: Existing Leads Exclusion (MANDATORY)

**ALWAYS run exclusion before enrichment.** Enriching leads that are already in your email platform wastes API credits. In one build, the exclusion rate was 31.7% - that's 31.7% of enrichment spend saved by running exclusion first.

Removes leads already in your email platform or CRM so only net new records proceed to enrichment. Prevents double-contacting prospects and wasting enrichment credits.

### How It Works

1. **Email platform exclusion**: Build a domain cache from all existing leads in your email sending platform using async parallel fetching (e.g., aiohttp with 20 concurrent requests).
2. **CRM/database exclusion**: Query your CRM or database for all known domains.
3. **Merge**: Combine both domain sets into a single exclusion list.
4. **Filter**: Remove TAM records whose domain matches the exclusion set.
5. **Output**: `net_new_leads.csv` + exclusion stats in `dedup_stats.json`.

### Performance

Async fetching with 20 concurrent requests achieves ~7-8 pages/sec (vs ~0.4/sec sync). For large workspaces:

| Workspace Size | Pages | Sync Time | Async Time |
|---|---|---|---|
| 79K leads | ~5,300 | ~15-20 min | ~11 min |
| 204K leads | ~13,600 | ~95 min | ~28 min |

### Output Stats

The exclusion stats show exactly how much TAM is already contacted:

```
TAM input:              39,721
Excluded (domain):      10,870
Excluded (email):        1,711
Net new leads:          27,140
Exclusion rate:          31.7%
```

### Cache

- Store domain cache locally (e.g., `./cache/platform_domains.json`)
- Contains all unique domains and emails from your email platform
- Auto-refresh after 24 hours
- Force rebuild when needed
- **Use workspace-specific API keys** if running multiple client workspaces

---

## Phase 5: Enrichment Hand-off

### Pre-Flight Checks (BEFORE starting enrichment)

1. **Check email verification credits**: Ensure your email verification service (e.g., MillionVerifier, ZeroBounce) has sufficient credits - budget for ~1 credit per email, with 30-50% of total leads having emails.
2. **Estimate enrichment volume**: After exclusion, how many leads need enrichment? If >10K, plan for batched processing.
3. **Check API availability**: Ensure all enrichment API keys are valid and credits/limits are sufficient.

### Adaptive Email Waterfall

For large TAMs (>5K leads), sample before committing to the full waterfall:

1. **Sample 100-200 domains** from the net new CSV
2. **Run email finding** on the sample only
3. **Measure hit rate** - if generic emails (info@, contact@) hit >60%, the full waterfall is worth running. If <30%, consider:
   - Skipping personal email search (expensive, low yield for local businesses)
   - Going straight to pattern-based generic email verification
   - Focusing enrichment budget on the highest-value segments

### Post-Enrichment Verification

**ALWAYS verify emails before campaign prep.** MX-guess generic emails are ~45% undeliverable.

- Keep: valid (code 1) + catch_all (code 2)
- Drop: unknown (3), error (4), disposable (5), invalid (6)

### After Enrichment

The enriched output feeds into the standard campaign workflow:
1. **Segment** by geography, company size, or industry vertical
2. **Write copy** personalized per segment
3. **Launch** campaigns

---

## Cost Model

| Component | Cost Driver | Typical Estimate |
|---|---|---|
| Serper queries | ~$0.004/query | 2,000 queries = ~$8 |
| IcyPeas | Credits per company | Varies by plan |
| SAM.gov | Free public API | $0 |
| Email enrichment (unlimited plan) | Monthly subscription | $0 marginal |
| Email verification | ~$0.001/email | $0.001 x email count |
| Google Maps ZIP scrape | Serper queries | ~$0.004/ZIP x 40K ZIPs = ~$160 for nationwide |

Typical TAM build: **$10-20 in API costs** for 50K-100K records (excluding ZIP scrape).

---

## Reference Builds

### Roofing TAM (First Build)

| Metric | Value |
|---|---|
| Data sources | 20+ |
| Raw records | 113,000+ |
| After dedup | 89,562 |
| With owner names | 31,212 (34.8%) |
| Sendable (verified email) | 20,557 |
| Total cost | ~$15 |
| Top sources | State licenses (44K), IcyPeas (33K), Google Maps (12K), Clay.com (7K) |

### Coffee Shop TAM (Second Build)

| Metric | Value |
|---|---|
| Data sources | IcyPeas (4 keywords) + Google Maps ZIP scrape (3 keywords) |
| IcyPeas raw records | ~90,000 (coffee shop + cafe + coffee roaster + espresso bar) |
| ZIP scrape raw records | 49,811 (cafe + coffee roaster + espresso bar, nationwide) |
| After cross-source dedup | 39,721 |
| After platform exclusion | 27,140 (31.7% already contacted) |
| Sendable (verified) | 11,206 (41% of net new) |
| ZIP scrape net new (addl) | 13,667 domains for enrichment |
| Keyword expansion effect | Primary keyword alone missed ~35% of market |
| Pattern recovery (unsendable) | 0/15,934 - generic patterns don't work for single-location businesses |
| Key insight | Dedup before enrichment saved 31.7% of enrichment spend |
| Key insight | Keyword expansion (cafe, roaster, espresso) found ~13K net new domains |
| Key insight | Pattern-based email recovery (info@, contact@, etc.) yielded 0% on unsendable domains |

## Important Notes

- **Source discovery is the bottleneck, not scraping.** Spend the most time on Phase 1. A TAM is only as good as its source coverage.
- **State license databases are gold for local services.** They often include owner names, which bypasses the most expensive enrichment step.
- **Always verify emails before sending.** MX-guess generic emails are ~45% undeliverable. Keep valid (code 1) + catch_all (code 2), drop everything else.
- **IcyPeas /find-companies/count is free** - use it to estimate volume before committing credits.
- **Every scraper outputs businesses.csv** with the unified schema. The dedup engine auto-maps columns.
- **Bespoke scrapers get saved** to `sources/{vertical}/` for reuse on future builds.
- **ALWAYS run exclusion (Phase 4.5) before enrichment.** Saves 20-40% of enrichment spend by not re-enriching already-contacted leads.
- **Keyword expansion (Phase 1.5) is high leverage for local businesses.** Adjacent terms (cafe vs coffee shop, roaster vs coffee roaster) can uncover 30-60% more of the market.
- **Pattern-based email recovery does NOT work for single-location businesses.** Tested 10 patterns x 15,934 domains = 0 hits. These businesses simply don't have functional generic email addresses.
- **Use workspace-specific API keys** for exclusion if running multiple client workspaces.
