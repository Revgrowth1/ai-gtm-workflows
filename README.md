# AI GTM Workflows

12 AI-powered Go-To-Market workflows for B2B outbound. Clone the repo, add your API keys, run with [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

These workflows cover the full GTM lifecycle - from market research to campaign optimization - and are designed to run as Claude Code skills. Each workflow is a structured SKILL.md file that Claude follows step-by-step.

## What's Inside

| # | Workflow | What It Does |
|---|---------|-------------|
| **Research & Strategy** | | |
| 01 | [Market Research](workflows/01-market-research/) | 9-dimension company analysis via web search |
| 02 | [TAM Mapping](workflows/02-tam-mapping/) | Build a total addressable market database from multiple sources |
| 03 | [ICP Scoring](workflows/03-icp-scoring/) | Score companies 0-100 against your ideal customer profile |
| 04 | [GTM Strategy](workflows/04-gtm-strategy/) | Full pipeline: research, segments, personas, messaging, copy |
| **Prospecting & Angles** | | |
| 05 | [Situation Mining](workflows/05-situation-mining/) | Infer prospect worldview for diagnostic (not promotional) messaging |
| 06 | [Creative Angles](workflows/06-creative-angles/) | Discover hidden outbound signals via lateral thinking models |
| 07 | [Message-Market Fit](workflows/07-message-market-fit/) | MSPA framework for systematic message testing |
| **List Building & Enrichment** | | |
| 08 | [Contact Discovery](workflows/08-contact-discovery/) | Domain to LinkedIn to verified email - waterfall enrichment |
| 09 | [Local Enrichment](workflows/09-local-enrichment/) | Google Maps scraping to campaign-ready local business leads |
| **Campaign Execution & Optimization** | | |
| 10 | [Campaign Launch](workflows/10-campaign-launch/) | CSV to segmented, sender-attached campaigns |
| 11 | [Performance Analysis](workflows/11-performance-analysis/) | 5 Variables framework for diagnosing campaign performance |
| 12 | [Campaign Debrief](workflows/12-campaign-debrief/) | Structured learning capture after campaigns complete |

## Quick Start

### Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (Anthropic's CLI for Claude)
- An [Anthropic API key](https://console.anthropic.com/)
- Additional API keys depending on which workflows you use (see `.env.example`)

### Setup

```bash
# Clone the repo
git clone https://github.com/Revgrowth1/ai-gtm-workflows.git
cd ai-gtm-workflows

# Set up your environment
cp .env.example .env
# Edit .env with your API keys

# Run any workflow with Claude Code
claude
# Then: "Run the market research workflow for [company name]"
```

### Running a Workflow

Each workflow lives in `workflows/XX-name/SKILL.md`. You can:

1. **Ask Claude directly**: "Run the market research workflow for Stripe"
2. **Reference by path**: "Follow the instructions in workflows/04-gtm-strategy/SKILL.md for my SaaS product"
3. **Chain workflows**: "Research Acme Corp, then build a GTM strategy, then create campaign copy"

## Workflow Details

### Phase 1: Research & Strategy

**01 - Market Research**: Runs a 9-dimension analysis of any company using web search. Covers business model, product/market fit signals, competitive landscape, hiring patterns, technology stack, leadership, funding, partnerships, and market positioning. Outputs a structured research brief.

**02 - TAM Mapping**: Methodology for building a total addressable market from multiple data sources (company databases, LinkedIn, industry directories, web scraping). Produces a scored and deduplicated company list.

**03 - ICP Scoring**: Takes a list of companies and scores each 0-100 against your ideal customer profile criteria. Uses weighted scoring across firmographic, technographic, and behavioral dimensions.

**04 - GTM Strategy**: The big one. 5-phase pipeline that takes a product/service and produces segments, personas, messaging angles, and ready-to-send campaign copy. This is a full strategy engagement compressed into a single workflow.

### Phase 2: Prospecting & Angles

**05 - Worldview Mining**: Infers what a prospect's world looks like from the inside - their daily frustrations, metrics they're judged by, political dynamics, and hidden constraints. Produces "worldview briefs" that power diagnostic (not promotional) outreach.

**06 - Creative Angles**: Uses lateral thinking models to discover non-obvious outbound angles. Instead of "we do X" messaging, finds hidden signals (hiring patterns, tech migrations, regulatory changes) that create natural entry points. Includes reference files with thinking models and signal libraries.

**07 - Message-Market Fit**: Implements the MSPA (Message, Segment, Proof, Ask) framework for systematically testing which messages resonate with which segments. Designed for iterative testing, not one-shot campaigns.

### Phase 3: List Building & Enrichment

**08 - Contact Discovery**: Waterfall enrichment methodology - starts with a company domain, finds employees via LinkedIn, discovers and verifies email addresses through multiple sources, and outputs campaign-ready contact lists. Includes verification cascade to maximize deliverability.

**09 - Local Business Enrichment**: Specialized workflow for local/SMB businesses. Scrapes Google Maps for businesses matching your criteria, enriches with website data and owner information, verifies emails, and produces campaign-ready lists. Optimized for businesses that don't have strong LinkedIn presence.

### Phase 4: Campaign Execution & Optimization

**10 - Campaign Launch**: Takes a CSV of enriched contacts and turns it into segmented campaigns with senders attached and schedules configured. Handles deduplication, custom variable mapping, and multi-campaign orchestration.

**11 - Performance Analysis**: Applies the 5 Variables framework (List, Offer, Copy, Deliverability, Timing) to diagnose why a campaign is or isn't working. Produces specific, actionable recommendations rather than generic "improve your subject line" advice.

**12 - Campaign Debrief**: Structured learning capture that runs after a campaign completes (or is paused). Captures what worked, what didn't, and specific hypotheses to test next. Designed to compound knowledge across campaigns rather than starting fresh each time.

## Reference Files

The `references/` directory contains shared resources used by multiple workflows:

- **`research-processes/`** - Search query patterns for different research dimensions (finding competitors, growth signals, hiring patterns, etc.)
- **`creative-thinking-models.md`** - Lateral thinking frameworks used by the creative angles workflow
- **`hidden-signals-library.md`** - Catalog of non-obvious buying signals
- **`shelf-life-patterns.md`** - How long different signals remain relevant

## Tool Stack

These workflows are designed to work with Claude Code and standard APIs. The specific tools you'll need depend on which workflows you run:

| Category | What You Need | Used By |
|----------|--------------|---------|
| AI | Claude Code + Anthropic API key | All workflows |
| Enrichment | Any B2B enrichment API (Apollo, Clearbit, etc.) | 08, 09 |
| Email Verification | Any SMTP verification service (MillionVerifier, ZeroBounce, etc.) | 08, 09 |
| Email Platform | Any cold email platform with API (Instantly, Smartlead, etc.) | 10, 11 |
| Data | Google Maps API (optional, for local enrichment) | 09 |

## Customization

### Client Configuration

Copy `examples/client-config.yaml` to `clients/{your-client}/config.yaml` and customize. The config file defines:
- ICP criteria (for scoring and targeting)
- Market segments (for campaign segmentation)
- Offers (for message rotation)
- Platform settings (send limits, schedules)

### Adapting Workflows

Each SKILL.md is a self-contained instruction set. You can:
- Modify scoring weights in ICP Scoring to match your criteria
- Add new research dimensions to Market Research
- Customize the MSPA framework variables in Message-Market Fit
- Adjust the 5 Variables analysis framework in Performance Analysis

## Philosophy

These workflows are built on a few core beliefs:

1. **Diagnostic over promotional** - The best outbound doesn't pitch. It demonstrates understanding of the prospect's world. Situation Mining and Creative Angles exist specifically for this.

2. **Compounding over one-shot** - Campaign Debrief captures learnings. Performance Analysis identifies specific variables to test. Each campaign makes the next one better.

3. **Full lifecycle** - Most GTM tools help with one phase. These workflows cover research through optimization, so insights compound across the entire lifecycle.

4. **AI-native** - These aren't templates you fill in. They're structured workflows that Claude follows autonomously, making decisions and producing output at each step.

## License

MIT - use these however you want.

## Credits

Built by [RevGrowth](https://revgrowth.ai). Message-Market Fit framework inspired by Kellen Casebeer's diagnostic selling methodology.
