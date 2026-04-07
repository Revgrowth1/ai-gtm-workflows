# AI GTM Workflows - Claude Code Project Instructions

This repo contains 12 GTM (Go-To-Market) workflows designed to run as Claude Code skills.

## How to Use

Each workflow lives in `workflows/XX-workflow-name/SKILL.md`. To run a workflow:

1. Open this repo as your working directory in Claude Code
2. Tell Claude which workflow you want to run (e.g., "Run the market research workflow for [company]")
3. Claude will read the SKILL.md and follow its instructions

## Workflow Sequence

The workflows follow a natural GTM lifecycle. You don't need to run all of them - pick what fits your stage:

**Research & Strategy (start here)**
1. `01-market-research` - Deep company analysis (9 dimensions via web search)
2. `02-tam-mapping` - Build your total addressable market database
3. `03-icp-scoring` - Score companies against your ideal customer profile
4. `04-gtm-strategy` - Full strategy: segments, personas, messaging, copy

**Prospecting & Angles (refine your approach)**
5. `05-situation-mining` - Infer prospect worldview for diagnostic messaging
6. `06-creative-angles` - Discover hidden signals via lateral thinking
7. `07-message-market-fit` - Systematic message testing framework (MSPA)

**List Building & Enrichment (build your lists)**
8. `08-contact-discovery` - Domain to LinkedIn to verified emails
9. `09-local-enrichment` - Google Maps to campaign-ready local business leads

**Campaign Execution & Optimization (launch and learn)**
10. `10-campaign-launch` - CSV to segmented, sender-attached campaigns
11. `11-performance-analysis` - 5 Variables framework for campaign analysis
12. `12-campaign-debrief` - Structured learning capture after campaigns end

## Environment

- API keys are loaded from `.env` in the repo root (copy `.env.example` to `.env`)
- Reference files used by multiple workflows live in `./references/`
- Output files are saved to `./clients/{client-name}/` by default

## Conventions

- Workflows reference each other by path (e.g., `./workflows/01-market-research/`)
- Client-specific output goes in `./clients/{client-slug}/`
- All API integrations use environment variables - never hardcode keys
