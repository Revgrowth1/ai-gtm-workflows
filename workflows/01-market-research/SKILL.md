---
name: research
description: Run validated search processes against a company or person. USE WHEN user says "research" OR "research [company]" OR "deep research" OR "find info on" OR "company research" OR "people research" OR wants structured company intelligence.
---

# Research

Run validated search processes from `./references/research-processes/`. Each process has been tested across 25 companies, 4 tiers, 3,357+ searches with 90%+ accuracy.

## Input

- `company_name` - required
- `domain` - required (used for site: searches)
- `category` - what they do in 2-3 words (optional but improves accuracy for ambiguous names)
- `mode` - which processes to run (default: `profiles`)

## Modes

| Mode | Processes | Searches | Use Case |
|------|-----------|----------|----------|
| `profiles` | find-profiles | 3-6 | Quick company overview |
| `competitors` | find-competitors | 2-5 | Competitive landscape |
| `growth` | find-growth-signals | 3-8 | Marketing maturity assessment |
| `hiring` | find-hiring | 2-4 | Growth trajectory via jobs |
| `reviews` | find-reviews | 3-6 | Customer and employee sentiment |
| `news` | find-news | 2-5 | Recent events and announcements |
| `negativity` | find-negativity | 3-6 | Complaints and pain points |
| `founders` | find-founders | 2-4 | Founder/CEO identification |
| `c-suite` | find-c-suite | 3-6 | Executive team mapping |
| `full` | profiles + competitors + growth + hiring | 10-23 | Core company intelligence |
| `deep` | All 9 company processes | 25-50 | Comprehensive company research |
| `people` | founders + c-suite + directors + vp-leadership + department-heads + specialist-roles + people-creative | 20-40 | Full org chart discovery |

## Execution Flow

1. User provides company_name, domain, and optional category/mode
2. Read the process file(s) from `./references/research-processes/`
3. Fill `{{variable}}` placeholders:
   - `{{company_name}}` - from input
   - `{{domain}}` - from input
   - `{{category}}` - from input (omit from query if not provided)
   - `{{current_year}}` - current year
4. Execute searches using Serper (web search API) following each process's step order
5. Follow **stop conditions** - skip remaining steps when conditions are met
6. Respect **kill lists** - never run queries marked as KILL or in "do not search"
7. Extract data points specified in each step's "extract from results" section
8. Format output using the process file's output template

## Key Rules

- **Follow stop conditions** - don't waste searches when you already have the data
- **Respect kill lists** - these queries are validated as ineffective or misleading
- **Use the PRIMARY query pattern first** - it's the highest-accuracy pattern per validation
- **Category qualifier improves accuracy** for ambiguous company names (Clay, Stripe, etc.)
- **Tier awareness** - T3/T4 (smaller companies) have thinner data for news, media, specialized roles. Don't chase what doesn't exist.
- **Rate limit** - pause 150ms between searches

## Process Files Reference

**Company processes:**
- `find-profiles.md` - company overview, funding, size, category
- `find-competitors.md` - competitive landscape, alternatives, positioning
- `find-growth-signals.md` - marketing infrastructure, content, social, community
- `find-hiring.md` - careers page, ATS boards, hiring velocity
- `find-news.md` - recent announcements, events, launches
- `find-negativity.md` - complaints, criticism, pain points
- `find-reviews.md` - customer and employee reviews, sentiment
- `find-pr-releases.md` - press releases, official communications

**People processes:**
- `find-founders.md` - CEO, founders, co-founders
- `find-c-suite.md` - CTO, CMO, CRO, CPO, CISO, CFO, COO
- `find-vp-leadership.md` - VP Sales, VP Marketing, VP Engineering
- `find-directors.md` - Director-level across Sales, Marketing, Engineering
- `find-department-heads.md` - Head of Growth, RevOps, Customer Success
- `find-specialist-roles.md` - HR, Finance/Legal, Technical ICs
- `find-people-creative.md` - people via media, platforms, authored content
- `find-job-role-insights.md` - deep dive on specific job postings (companion to find-hiring)

## Output

Use each process file's output template verbatim. For multi-process modes (`full`, `deep`, `people`), concatenate outputs with `---` separators.

After outputting, offer to save to client folder: `./clients/{client}/research-{date}.md`

## Cost

- Serper: ~$0.001/search
- `profiles` mode: ~$0.005
- `full` mode: ~$0.02
- `deep` mode: ~$0.05
- `people` mode: ~$0.04
