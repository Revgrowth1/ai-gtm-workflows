---
name: icp-verify
description: Score companies against client ICP criteria using web search + LLM. Replaces manual qualifying filters.
---

# ICP Verify

Parallel research (20 workers) to score companies 0-100 against ICP criteria. Outputs qualified/disqualified CSVs.

## Usage

```
icp_verify.py companies.csv \
  --client {client_slug}                # Load ICP from client knowledge base
  --criteria "B2B SaaS, 50-500, US"     # OR inline criteria
  --criteria-file ./criteria.json       # OR JSON file
  --threshold 70                        # Min score (default: 60)
  --preview                             # Sample 5 companies
  --output DIR                          # Output dir
  --workers 20                          # Parallel workers
```

IMPORTANT: At least one of `--client`, `--criteria`, or `--criteria-file` required.

## ICP Criteria Sources

1. **Auto**: `./clients/{client}/context.md` ICP section
2. **JSON**: `{"industry":[], "employee_range":{}, "geography":[], "must_have":[], "must_not_have":[], "signals":[], "description":""}`
3. **Inline**: Description string via `--criteria`

## Scoring

|Score|Label|
|---|---|
|80-100|Strong Match|
|60-79|Likely Match|
|40-59|Partial Match|
|0-39|Poor Match|

## Required CSV Columns

|Column|Required|
|---|---|
|`company_name` or `company`|Yes|
|`domain` or `company_domain`|Yes|
|`industry`|No (pre-filter)|
|`employees` or `employee_count`|No (pre-filter)|

## Flow

1. Read CSV, validate columns
2. Load ICP criteria (client context / manual / JSON)
3. Pre-filter by known columns (reduces API calls)
4. Research companies in parallel (20 workers, web search, checkpoint every 100)
5. LLM score 0-100 with reasoning
6. Split -> `{file}_qualified.csv` + `{file}_disqualified.csv`
7. Report summary + score distribution + top disqualification reasons

## Output Columns Added

`icp_score`, `icp_label`, `icp_reasoning`, `company_summary`

## Cost

|Companies|Est. Cost|Est. Time|
|---|---|---|
|100|~$1.50|~2 min|
|500|~$7.50|~8 min|
|1,000|~$15|~15 min|

## Error Handling

|Error|Action|
|---|---|
|Missing domain column|Exit with error|
|Search rate limit (429)|Wait 3s, retry|
|LLM timeout|Conservative score (40)|
|No client context|Prompt for manual criteria|
|Empty search results|Score on available data, flag low-confidence|

## Configuration

Keys from `.env`: `SERPER_API_KEY`, `OPENROUTER_API_KEY` (or your preferred LLM provider)

## Related Workflows

- `./workflows/04-gtm-strategy/` (generates ICP criteria)
- Enrichment pipeline (next step after qualifying)
