---
name: contact-discovery
description: Contact enrichment pipeline - Domain to LinkedIn to ICP decision-makers to verified emails. Waterfall enrichment with multiple API fallbacks. USE WHEN you need to find C-suite/VP/Director contacts from a list of company domains.
---

# Contact Discovery Pipeline

Domain -> LinkedIn Company URL -> ICP Decision-Makers -> Verified Work Emails. Uses a waterfall enrichment pattern with primary enrichment API and email fallbacks.

## 3-Step Pipeline

|Step|What It Does|Credits|
|---|---|---|
|1|Domain -> LinkedIn company URL|1/domain|
|2|Waterfall ICP search -> decision-maker contacts|1/contact found|
|3|Email waterfall (primary enrichment API -> LinkedIn enrichment API -> keyword search API)|1/email (primary only)|

## Default ICP Cascade (configurable)

|Tier|Titles|
|---|---|
|1|CEO, Founder, Owner, President, Co-Founder|
|2|VP Marketing, VP Sales, VP Growth, CMO, CRO|
|3|Marketing Director, Sales Director, Director of Growth|

Max 3 contacts per company. Custom cascade via `--cascade-json`.

## Execution

```bash
# Standard run
python3 ./workflows/08-contact-discovery/contact_discovery.py input.csv -o contacts.csv

# Dry run (estimate credits without calling APIs)
python3 ./workflows/08-contact-discovery/contact_discovery.py input.csv --dry-run

# Limit companies, skip email step
python3 ./workflows/08-contact-discovery/contact_discovery.py input.csv -o contacts.csv --max-companies 50 --skip-email

# More contacts per company
python3 ./workflows/08-contact-discovery/contact_discovery.py input.csv -o contacts.csv --max-results 5
```

## Input CSV

Needs a domain column (auto-detected from: `domain`, `website`, `company_domain`, `url`, `website url`, `company website`). Optional `company` / `company name` column.

## Output

Creates `{input}_enriched.csv` with columns: `company`, `domain`, `company_linkedin_url`, `first_name`, `last_name`, `full_name`, `job_title`, `linkedin_headline`, `person_linkedin_url`, `email`, `email_source`, `all_emails`, `country`, `person_city`, `icp_tier`, `what_matched`.

Also saves raw JSON for debugging.

## API Keys

Resolved: CLI flag -> env var -> `./.env`.

|Key|Required|Purpose|
|---|---|---|
|`PRIMARY_ENRICHMENT_API_KEY`|Yes|All 3 steps|
|`LINKEDIN_ENRICHMENT_API_KEY`|No|Email fallback #1|
|`KEYWORD_SEARCH_API_KEY` + `KEYWORD_SEARCH_API_SECRET`|No|Email fallback #2|

## Waterfall Enrichment Pattern

The key methodology here is **waterfall enrichment**: try the primary source first, then cascade through fallbacks. This maximizes coverage while minimizing cost (cheaper sources are tried first).

```
Primary Enrichment API (cheapest, broadest)
    |-- Found? -> Done
    |-- Not found? -> LinkedIn Enrichment API (higher quality for LinkedIn-sourced leads)
        |-- Found? -> Done
        |-- Not found? -> Keyword Search API (niche coverage)
            |-- Found? -> Done
            |-- Not found? -> Mark as "no email found"
```

Each source returns different confidence levels. Track `email_source` so you can analyze which sources produce the best deliverability rates downstream.
