---
name: local-enrichment
description: Local business owner enrichment pipeline - Google Maps scraping, owner finding, email discovery. 97% cheaper than Clay. USE WHEN you need to build a lead list from Google Maps searches, find business owners, or enrich local business leads.
---

# Local Business Owner Enrichment Pipeline

End-to-end pipeline: Google Maps search -> Owner identification -> Email discovery -> Campaign-ready segmentation. 97% cheaper than Clay with 81% email coverage. Includes lead scoring, MX host classification, and cost tracking.

## 4-Stage Pipeline

|Stage|Script|What It Does|
|---|---|---|
|1|`1_scrape_maps.py`|Scrape Google Maps via Serper API for business listings|
|2|`2_find_owners.py`|5-layer waterfall to identify business owners (LinkedIn, enrichment API, web scraping, Facebook, state registries, LLM)|
|3|`3_find_emails.py`|Parallel email waterfalls for personal + generic emails (LinkedIn enrichment API, keyword search API, primary enrichment API, email verification API)|
|4|`4_prepare_campaigns.py`|Score leads (A/B/C tiers), classify email hosts via MX, segment into campaign-ready CSVs|

## Execution

```bash
# Full pipeline - query + location
python3 ./workflows/09-local-enrichment/run_pipeline.py --query "plumbers" --location "Dallas, TX"

# Bulk mode - query file (one per line, or query|location)
python3 ./workflows/09-local-enrichment/run_pipeline.py --query-file queries.txt

# Nationwide ZIP code scraping (one query per US ZIP code)
python3 ./workflows/09-local-enrichment/run_pipeline.py --query "Juice bar" --zip-file ./workflows/09-local-enrichment/data/us_zipcodes.txt --max-results 20

# Resume interrupted ZIP scrape
python3 ./workflows/09-local-enrichment/run_pipeline.py --query "Juice bar" --zip-file ./workflows/09-local-enrichment/data/us_zipcodes.txt --resume

# Start from existing CSV (skip Maps scraping)
python3 ./workflows/09-local-enrichment/run_pipeline.py --input existing.csv

# Run a single step
python3 ./workflows/09-local-enrichment/run_pipeline.py --query "plumbers" --location "Dallas, TX" --step 1

# Resume interrupted pipeline
python3 ./workflows/09-local-enrichment/run_pipeline.py --query "plumbers" --location "Dallas, TX" --resume
```

## Key Options

|Flag|Default|Purpose|
|---|---|---|
|`--zip-file`|-|ZIP code mode: text file with one ZIP per line, generates one query per ZIP|
|`--max-results`|100|Max Maps results per query (use 20 for ZIP mode)|
|`--max-workers`|1|Thread pool size for steps 2-3|
|`--step 1\|2\|3\|4`|all|Run only a specific step|
|`--resume`|off|Resume from checkpoints (includes ZIP scrape checkpoint)|
|`--skip-verify`|off|Skip email verification|
|`--cost-file`|auto|Path to cost tracking JSON (auto-created in output dir)|
|`-o, --output-dir`|auto|Custom output directory|

## Output

Creates a dated directory under `./output/` containing:

|File|Contents|
|---|---|
|`businesses.csv`|Step 1 - scraped business listings|
|`businesses_with_owners.csv`|Step 2 - listings + identified owners|
|`businesses_enriched.csv`|Step 3 - full enrichment with emails (+ `lead_score`, `lead_tier` after Step 4)|
|`campaigns/`|Step 4 - campaign-ready CSVs segmented by email host x lead tier|
|`campaigns/segment_summary.json`|Step 4 - segment counts, tier/host distributions, sendable rate|
|`cost_tracking.json`|API call counts and costs across all steps|
|`stats.json`|Pipeline statistics|

## Step 4: Campaign Preparation

Step 4 transforms enriched leads into campaign-ready CSVs. Three operations:

1. **Lead Scoring** (0-100, A/B/C tiers): Owner confidence (40pts), email quality (35pts), data completeness (15pts), business signals (10pts). Tiers: A >= 70, B >= 40, C < 40.
2. **MX Classification**: Resolves email domains via DNS MX records to classify as google/microsoft/other. Threaded batch resolution with domain-level caching.
3. **Segmentation**: Splits leads by email_host x lead_tier into campaign CSVs (e.g. `google_tier_a.csv`, `microsoft_tier_b.csv`). Small segments merge into `{host}_mixed` or `other_mixed`. Generic-only leads go to `generic_email.csv`. Unsendable leads go to `unsendable.csv`.

Campaign CSV columns match standard email platform format: `email`, `first_name`, `last_name`, `company_name`, `job_title`, `company_domain`, `phone`, `address`, `category`, `lead_score`, `lead_tier`.

## API Keys

Resolved in order: CLI flag -> env var -> `./.env`.

|Key|Used In|
|---|---|
|`SERPER_API_KEY`|Steps 1, 2|
|`PRIMARY_ENRICHMENT_API_KEY`|Steps 2, 3|
|`LLM_ENDPOINT`, `LLM_API_KEY`, `LLM_MODEL`|Step 2 (owner extraction via LLM)|
|`LINKEDIN_ENRICHMENT_API_KEY`|Step 3|
|`KEYWORD_SEARCH_API_KEY`, `KEYWORD_SEARCH_API_SECRET`|Step 3|
|`EMAIL_VERIFICATION_API_KEY`|Step 3 (email verification)|

## Important Notes

- **ALWAYS verify emails** before sending campaigns (don't use `--skip-verify` for production lists)
- **ZIP mode** uses a ZIP code file (40,781 US ZIP codes) for nationwide coverage. Use `--max-results 20` (most ZIPs have few results per vertical). Checkpoints every 100 queries, progress every 500.
- Step 2 uses LLM analysis - configure `LLM_ENDPOINT` for owner extraction from web pages
- Checkpoints save progress per step - safe to interrupt and resume

## Waterfall Enrichment Methodology

The pipeline uses a **5-layer waterfall** for owner identification in Step 2:

```
Layer 1: LinkedIn (highest confidence - professional profiles)
Layer 2: Primary enrichment API (company data + people)
Layer 3: Web scraping (About pages, team pages)
Layer 4: Facebook business pages
Layer 5: State business registries + LLM extraction
```

For email discovery in Step 3, a **parallel waterfall** runs two tracks simultaneously:

```
Track A: Personal email          Track B: Generic email
  LinkedIn enrichment API          Pattern generation (info@, hello@)
  -> Keyword search API            -> MX verification
  -> Primary enrichment API
  -> Email verification API
```

This dual-track approach ensures you have both a personal email (higher reply rate) and a generic fallback (higher deliverability). The lead scoring in Step 4 weights personal emails higher.
