---
name: gtm-strategy
description: Generate GTM strategy docs with market research, TAM segmentation, personas, and campaign copy.
---

# GTM Strategy

5-phase pipeline: Research -> Segments -> Personas -> Copy -> Output. Uses web search research + client knowledge base context. Saves to `./clients/{client}/`.

## Usage

```
gtm_strategy.py \
  --client "Example Corp" --domain "example.com"

# Options
  --context "..."       # Additional onboarding context
  --phase 1             # Run specific phase only (1-5)
  --resume --phase 3    # Resume from saved state
  --preview             # Quick mode (3 segments, shorter research)
  --output DIR          # Output dir (default: ./clients/{client}/)
  --max-segments N      # Max segments (default: 7, max: 10)
```

## Phases

|Phase|What|Output|
|---|---|---|
|1. Market Research|Web searches + LLM analysis (company, competitors, landscape)|Structured JSON|
|2. TAM Segments|3-10 industry segments with NAICS, scoring (size, fit 2x weight, cycle, deal value, education)|Ranked segments|
|3. Deep Dive|Per-segment: 3 personas, PQS, 9+ data sources, buying behavior|Persona + PQS JSON|
|4. Copywriting|Per-segment email scripts with personalization vars, spintax, <70 words, soft CTA|3-6 scripts/segment|
|5. Output|Strategy markdown + state JSON for resume|`gtm-strategy.md`|

## Personalization Variable Rules

Standard variables: `{FIRST_NAME}`, `{COMPANY}`, `{INDUSTRY}`, `{LOCATION}`, `{PERSONA_ROLE}`, `{PRIMARY_KPI}`, `{PEER_COMPANY}`, `{PAIN_POINT}`, `{OFFER_TYPE}`, `{RESEARCH_INSIGHT}`, `{PQS_TRIGGER}`

IMPORTANT: Single curly braces, UPPERCASE. Max 3/sentence, 5/email. No `{FIRST_NAME}` in subject lines. Subject: 1-3 words, 3 spintax options.

## Segment Scoring Formula

Each segment is scored across 5 dimensions:

| Dimension | Weight | What It Measures |
|---|---|---|
| Market Size | 1x | Total addressable businesses in the segment |
| ICP Fit | 2x | How well the segment matches the client's ideal customer profile |
| Sales Cycle | 1x | Speed from first touch to close (shorter = higher score) |
| Deal Value | 1x | Average contract value for the segment |
| Education Required | 1x | How much the prospect needs to be educated on the solution (less = higher) |

Fit is weighted 2x because a large market with poor fit wastes more resources than a smaller market with strong fit.

## Cost

~$0.85 total for 7 segments (~12 API calls).

## Configuration

Keys from `.env`: `SERPER_API_KEY`, `OPENROUTER_API_KEY` (or your preferred LLM provider)

## Related Workflows

- `./workflows/01-market-research/` (run before for deeper company intelligence)
- `./workflows/03-icp-scoring/` (uses Phase 2 segments for scoring criteria)
- Campaign launch tooling (uses Phase 4 copy)
