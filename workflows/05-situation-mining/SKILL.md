---
name: situation-mine
description: Mine prospect situations for diagnostic messaging using Stealth Offer framework. USE WHEN user says "situation mine" OR "mine situations" OR "research [company] for outreach" OR "find angles for [company]" OR "diagnostic messaging for".
---

# Situation Mining

Gather public data -> infer situations -> generate diagnostic messaging.

IMPORTANT: Situations beat signals. Everyone emails the funded company. You email based on what their data reveals about their worldview.

## Data Collection (run in parallel)

Each source maps to a validated process file in `./references/research-processes/`. Use the PRIMARY query pattern from each file.

|Source|Process File|PRIMARY Query|What to Gather|
|------|-----------|-------------|-------------|
|Company profile|find-profiles.md|`{{company_name}} {{category}} company overview`|Industry, size, funding, category|
|Founder/CEO|find-founders.md|`{{company_name}} CEO OR founder interview OR podcast`|Posting frequency/topics, background, worldview|
|Job postings|find-hiring.md|`{{company_name}} careers`|Hiring SDRs? Engineers? Marketers? NO sales roles?|
|Growth signals|find-growth-signals.md|`site:{{domain}} blog OR pricing OR newsletter OR demo OR "free trial" OR "book a call"`|Content investment, marketing maturity, lead capture|
|Competitors|find-competitors.md|`{{company_name}} competitors`|Market position, alternatives, differentiation|
|Negativity|find-negativity.md|`{{company_name}} {{category}} complaints OR "negative reviews" OR problems OR issues`|Customer pain points, public friction|

**Rules:**
- Follow stop conditions from each process file - don't waste searches when data is sufficient
- Respect kill lists - never run queries marked in "do not search" sections
- If `{{category}}` is unknown, omit it from queries (most PRIMARY patterns work without it)
- For ambiguous company names (Clay, Stripe), category is critical for accuracy

## Worldview Inference Patterns

|Data Point|Inferred Worldview|Messaging Implication|
|----------|-----------------|---------------------|
|High revenue, low headcount|Max leverage per person|Talk efficiency, not hiring|
|Funded but not hiring|Bootstrap mentality despite capital|Respect scrappiness|
|CEO posting content|Believes in founder brand|"Amplify what you're doing"|
|No outbound team|Anti-outbound or no fit|Don't lead with "we do outbound"|
|Heavy blog investment|Content drives growth|Adjacent offering angle|
|Using [competitor]|Category-familiar, has opinions|Position against friction points|
|Serial founder|Pattern recognition, hates BS|Get to the point fast|
|Active hiring in sales|Growth mode, needs pipeline|Lead generation angle|
|Negative reviews about support|Overwhelmed team, scaling pain|"Handle the volume" angle|
|No competitors found|Niche/new category|Category creation messaging|

## Adjacent Offering Logic

|Investing In|Adjacent Offering|
|------------|-----------------|
|Content marketing|Distribution, amplification|
|Paid ads|Attribution, conversion|
|Sales team|Enablement, leads|
|Product-led growth|Expansion revenue, onboarding|
|SEO|New channels (Reddit, LLM ranking)|

## Output Structure

1. **Raw Data** - website, LinkedIn, funding, tech stack, jobs, competitors, negativity findings
2. **Situations Identified** - each with evidence, inferred worldview, messaging implication
3. **Diagnostic Messages** (3-4 options) - each with why it works and what to avoid
4. **Recommendations** - best angle, avoid list, test hypothesis, personalization hook, next actions

## Execution Flow

1. User provides company name/domain (and optionally category)
2. **GATHER** (parallel): Run 6 validated searches using PRIMARY queries from table above
3. **INFER**: Map data to worldview patterns, identify adjacent offerings, note contradictions
4. **GENERATE**: 3-4 diagnostic messages, explain why each works, flag what to AVOID
5. **OUTPUT**: Full report, offer to save to knowledge base

## API Usage
- **Serper** (primary, ~$0.001/search): 6 validated searches from process files above
- Total cost per prospect: ~$0.006
- **WebFetch** (backup): when full page content needed beyond search snippets
- Kill-list awareness: never run queries from process file "do not search" sections (e.g., `site:apollo.io`, `{{company_name}} annual report`, `site:youtube.com`)

IMPORTANT: Situations are inferences, not facts. Always frame as "Based on public data..." / "This suggests..." / "Test this hypothesis..."
