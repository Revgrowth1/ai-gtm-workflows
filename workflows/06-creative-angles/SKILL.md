---
name: creative-gtm
description: Generate ranked creative angles from hidden signals using lateral thinking. USE WHEN user says "creative-gtm" OR "creative angles" OR "hidden signals for" OR "GTM alpha" OR "creative outbound for" OR "non-obvious angles" OR "experimental campaigns for". Quick Mode (lightweight research + 5 forcing functions) or Deep Mode (situation-mine + worldview conflicts). Produces scored angles with evidence density, timing urgency, shelf life warnings, and handoff commands.
---

# /creative-gtm - Creative GTM Angle Generator

## Overview

Generates ranked creative outbound angles from hidden signals - non-obvious public data that reveals burning need before the prospect feels it. This is the "right brain" complement to standard campaign ideation.

**The #1 question this skill answers:** "What do I know about my best customers that no one else is using?"

**Core concepts:**
- **GTM Alpha** = knowing something competitors don't. Like financial alpha - if everyone knows it, it's priced in. If your outbound angle appears in a Clay template or a LinkedIn thought leader post, the alpha is gone.
- **Hidden Signals** = non-obvious public data that, when combined, reveal a prospect's burning need before they publicly express it. One data point is noise. Multiple data points forming a cluster is a signal.
- **Barbell Strategy** = 90% of campaigns should use proven patterns (standard campaign ideation). 10% should be experiments (`/creative-gtm`). The 10% is where breakthroughs come from.

**What makes this different from standard campaign ideation:**

| | Standard Campaign Ideation | `/creative-gtm` |
|---|---|---|
| Purpose | Scale what works (90%) | Discover what's next (10%) |
| Thinking | Deductive (known patterns inward) | Abductive (unexpected signals outward) |
| Input | Client context files | Live research + lateral thinking |
| Risk | Low - proven patterns | Higher - but downside is capped (small test) |
| Kill switch | "NEEDS WORK" (improve it) | "COMMODITY" (discard it entirely) |

---

## Trigger Phrases

- `/creative-gtm {domain}`
- `/creative-gtm deep {domain}`
- `creative angles for {domain}`
- `hidden signals for {domain}`
- `GTM alpha for {domain}`
- `creative outbound for {domain}`
- `non-obvious angles for {domain}`
- `experimental campaigns for {domain}`

---

## Quick Mode - `/creative-gtm {domain}`

Default mode. Lightweight research, fast output. Best for initial exploration or when you need angles quickly.

### Step 1 - Lightweight Research

Run 5 Serper searches in parallel (~$0.005 total):

| Search | What You're Looking For |
|--------|------------------------|
| `site:{domain} blog` | Content themes, stated priorities, what they think matters |
| `"{company}" reviews OR complaints` | Customer pain they haven't solved, gaps in their offering |
| `"{company}" competitors OR alternative` | Competitive positioning, who they're losing to and why |
| `"{company}" regulation OR compliance OR law` | Regulatory pressure, upcoming deadlines, industry shifts |
| `"{company}" hiring OR careers OR jobs` | Growth signals, capability gaps, strategic direction |

### Step 2 - Signal Extraction

Group findings into **2-3 signal clusters**. A signal cluster = multiple independent data points that together reveal something non-obvious.

For each cluster:
```
### Signal Cluster: {Name}

| Data Point | Source | Standalone Meaning |
|------------|--------|--------------------|
| {finding 1} | {search/url} | {what it means alone} |
| {finding 2} | {search/url} | {what it means alone} |
| {finding 3} | {search/url} | {what it means alone} |

**Combined Inference:** {What these data points TOGETHER reveal that no single one shows}
**Confidence:** HIGH / MEDIUM / LOW
```

**Rules:**
- Minimum 2 data points per cluster. Single data points are noise, not signals.
- Each data point must come from a different source type.
- The combined inference must be genuinely non-obvious - something a competitor scanning the same public data would likely miss.

### Step 3 - Creative Angle Generation

For each signal cluster, apply the **5 forcing functions** (see `./workflows/06-creative-angles/references/creative-thinking-models.md`):

1. **Inversion** - "What guarantees this prospect would never buy?" Invert each answer.
2. **Adjacent Transfer** - Take a winning strategy from a different industry, apply here.
3. **Timing Arbitrage** - What can you tell them before they feel the urgency themselves?
4. **Specificity Escalator** - Escalate from generic to hyper-specific until the angle feels uncomfortably personal.
5. **Ecosystem Gap Analysis** - Where does pain hide between their tools?

Generate **3-5 angles** total. Not every forcing function produces a winner - that's expected.

### Step 4 - Score & Output

Score each angle using the Asymmetry Score (see Scoring section below). Output using the Campaign Strategy template.

---

## Deep Mode - `/creative-gtm deep {domain}`

Richer research, worldview conflict analysis. Requires `/situation-mine` output in conversation context.

### Prerequisite Check

1. **Check conversation context** for `/situation-mine` output for this domain.
2. **If missing:** Display:
   > No situation-mine output found for `{domain}`. Deep Mode requires prospect worldview data.
   > Run `/situation-mine {domain}` first, then come back with `/creative-gtm deep {domain}`.
3. **If older than 14 days:** Display warning:
   > Situation-mine data for `{domain}` is {N} days old. Signals decay. Consider re-running `/situation-mine {domain}` for fresher data.

### Step 1 - Load Situation-Mine Output

Extract from conversation context:
- Raw data (website, LinkedIn, funding, tech stack, jobs)
- Inferred worldviews
- Diagnostic messages
- Contradictions noted

### Step 2 - Deep Signal Research

Run 7 additional Serper searches (~$0.012 total including Quick Mode searches):

| Search | What You're Looking For |
|--------|------------------------|
| `"{company}" site:g2.com OR site:trustpilot.com OR site:capterra.com` | Customer voice - what users love/hate |
| `"{company}" conference OR event OR summit 2025 2026` | Industry events - what they attend, sponsor, present at |
| `"{industry}" regulation OR compliance 2025 2026` | Regulatory shifts creating urgency across the sector |
| `"{company}" partnership OR integration OR ecosystem` | Adjacent market moves, who they're connecting to |
| `"{company}" hiring {key-role} OR "head of" OR "VP of"` | Talent signals - strategic pivots revealed by hiring |
| `"{company}" revenue OR funding OR valuation OR growth` | Financial signals - runway, growth rate, investor pressure |
| `"{company}" site:reddit.com OR site:news.ycombinator.com` | Community sentiment - unfiltered opinions |

### Step 3 - Worldview Conflict Analysis

Cross-reference situation-mine worldviews with deep signals. The richest angles live in contradictions:

```
### Worldview Conflict: {Name}

| Stated Worldview | Contradicting Signal | Source |
|------------------|---------------------|--------|
| {what they say/believe} | {data that contradicts it} | {url/search} |

**What This Means:** {The gap between stated worldview and reality = the angle}
**Messaging Implication:** {How to use this without being confrontational}
```

**Rules:**
- Contradictions are goldmines. A company saying "we're AI-first" while hiring 50 manual data entry roles reveals a gap you can address.
- Never weaponize contradictions. Frame as "I noticed X, which made me wonder about Y" - curiosity, not gotcha.
- Minimum 1 worldview conflict per Deep Mode output.

### Step 4 - Pattern Library Cross-Reference

Check `./workflows/06-creative-angles/references/hidden-signals-library.md` for known signal patterns in this prospect's industry. Flag any matches.

### Step 5 - Generate Angles

Generate **5-8 angles** using all 5 forcing functions plus worldview conflicts. Deep Mode should produce at least 2 angles that Quick Mode could not have surfaced.

### Step 6 - Score & Output

Score each angle using the Asymmetry Score. Flag shelf life on every ALPHA and PROMISING angle. Output using the Campaign Strategy template.

---

## Scoring System - Asymmetry Score

Every angle is scored on 6 dimensions with asymmetric weighting (novelty and evidence matter most):

| Dimension | Weight | Low (1-3) | Medium (4-6) | High (7-10) |
|-----------|--------|-----------|--------------|-------------|
| **Novelty** | 2x | Appears in Clay templates or common playbooks | Uncommon but discoverable with effort | No one is using this angle |
| **Evidence Density** | 2x | Single data point, high speculation | 2-3 data points, moderate inference | 4+ data points, strong inference chain |
| **Timing Urgency** | 1.5x | Evergreen, no time pressure | Seasonal or cyclical relevance | Deadline-driven, narrow window |
| **Execution Simplicity** | 1x | Requires custom tooling or complex data pipeline | Needs some manual research | Can build list in Clay/Apollo in <1 hour |
| **Shelf Life** | 1x | <1 month before competitors copy | 3-6 months | 6+ months, structural advantage |
| **Downside Cap** | 0.5x | Risk of negative brand perception | Neutral worst case | Worst case = they ignore the email |

**Weighted Score Formula:**

```
Score = (Novelty*2 + Evidence*2 + Timing*1.5 + Simplicity*1 + ShelfLife*1 + Downside*0.5) / 8
```

### Verdict Mapping

| Score | Verdict | Action |
|-------|---------|--------|
| 8.0+ | **ALPHA** | Test immediately. Small batch (50-100 prospects). Measure response rate before scaling. |
| 6.0-7.9 | **PROMISING** | Refine evidence density or timing, then test. |
| 4.0-5.9 | **INTERESTING** | Too creative for cold outbound. Redirect to content as a thought leadership piece. |
| Below 4.0 | **COMMODITY** | Discard entirely. This angle has no asymmetric upside. Use standard campaign ideation instead. |

### Shelf Life Warning

Every ALPHA and PROMISING angle MUST include:

```
Shelf Life: {estimate} - {reasoning}
Decay trigger: {what would kill this angle}
Refresh: {when to re-evaluate}
```

See `./workflows/06-creative-angles/references/shelf-life-patterns.md` for estimation methodology.

---

## Output Templates

### Campaign Strategy Format (default)

```markdown
# Creative GTM: {Domain}

Generated: {YYYY-MM-DD}
Mode: Quick / Deep
Research cost: ~${amount}

---

## Signal Clusters

### Cluster 1: {Name}

| Data Point | Source | Standalone Meaning |
|------------|--------|--------------------|
| ... | ... | ... |

**Combined Inference:** ...
**Confidence:** HIGH / MEDIUM / LOW

{repeat for each cluster}

---

## Worldview Conflicts (Deep Mode only)

### Conflict 1: {Name}

| Stated Worldview | Contradicting Signal | Source |
|------------------|---------------------|--------|
| ... | ... | ... |

**What This Means:** ...
**Messaging Implication:** ...

---

## ALPHA (8.0+) - Test Immediately

### Angle 1: {Name}

**The Angle:** {1-2 sentence description of the creative outbound approach}

**Signal Cluster:** {which cluster this came from}
**Forcing Function:** {which thinking model generated it}
**Evidence Chain:** {data point 1} + {data point 2} + {data point 3} -> {inference}

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Novelty (2x) | {n} | {why} |
| Evidence Density (2x) | {n} | {why} |
| Timing Urgency (1.5x) | {n} | {why} |
| Execution Simplicity (1x) | {n} | {why} |
| Shelf Life (1x) | {n} | {why} |
| Downside Cap (0.5x) | {n} | {why} |
| **Weighted Score** | **{n}** | **ALPHA** |

Shelf Life: {estimate} - {reasoning}
Decay trigger: {what would kill this angle}
Refresh: {when to re-evaluate}

**Draft Message Framework:**
> Subject: {subject line}
>
> {2-3 line email skeleton - not a full draft, just the structure}

**Data Collection Methodology:**
1. {Step to build the prospect list for this angle}
2. {Step to enrich with the signal data}
3. {Step to verify before sending}

---

## PROMISING (6.0-7.9) - Refine and Test

{same structure as ALPHA}

**Refinement suggestion:** {specific improvement to raise score}

---

## INTERESTING (4.0-5.9) - Redirect to Content

### Angle N: {Name}

{abbreviated scoring - just total score + verdict}

**Content redirect:** This angle works better as thought leadership than cold outbound.
-> Platform recommendation: {LinkedIn / newsletter / blog}
-> Hook line: "{opening hook for the content piece}"

---

## COMMODITY (Below 4.0) - Discarded

### Angle N: {Name}

Score: {n} - **COMMODITY**. This angle has no asymmetric upside. Everyone can find this.
-> Use standard campaign ideation for proven patterns instead.

---

## Data Collection Summary

| Angle | Primary Data Source | Enrichment Tool | Est. List Size | Build Time |
|-------|-------------------|-----------------|----------------|------------|
| {angle 1} | {source} | {tool} | {n} | {time} |
| ... | ... | ... | ... | ... |

---

## Recommended Next Steps

### Immediate
- Test ALPHA angles: small batch (50-100), measure reply rate
- Build campaigns for each ALPHA angle

### This Week
- Refine PROMISING angles, re-score, then test
- Write message sequences for selected angles

### Content Pipeline
- Hand off INTERESTING angles to content workflows
- Track which content pieces generate inbound interest (validates the angle for future outbound)

### Shelf Life Calendar
| Angle | Shelf Life | Refresh Date | Decay Trigger |
|-------|-----------|--------------|---------------|
| ... | ... | ... | ... |

---

## Handoff Commands

- Build full campaign from an ALPHA angle
- Generate email sequences for selected angles
- Convert INTERESTING angles to thought leadership
- Launch test batches at scale
- Absorb proven angles post-test into the 90% playbook
- Analyze results after test to measure actual alpha
```

### Content Format

When user specifies content output (or when redirecting INTERESTING angles):

```markdown
# Creative Angles -> Content Frameworks: {Domain}

Generated: {YYYY-MM-DD}

---

## Framework 1: {Angle Name}

**Hook Line:** "{opening line that stops the scroll}"
**Core Insight:** {the non-obvious thing you discovered, stated as a takeaway}
**Supporting Data:**
- {data point 1 - specific, cited}
- {data point 2 - specific, cited}
- {data point 3 - specific, cited}

**Platform Recommendation:** {LinkedIn / Newsletter / Blog / Twitter thread}
**Why This Platform:** {match between content type and platform strength}

**Suggested Structure:**
1. {Hook - the counterintuitive opener}
2. {Setup - why conventional wisdom is wrong}
3. {Evidence - your signal cluster data}
4. {Framework - the reusable insight}
5. {CTA - what the reader should do next}

**Estimated Engagement:** {LOW / MEDIUM / HIGH} - {reasoning based on novelty + relevance}

---

{repeat for each angle}
```

---

## Integration Map

### Reads From (Upstream)

| Skill | What It Provides | Required? |
|-------|-----------------|-----------|
| `./workflows/05-situation-mining/` | Worldview data, contradictions, diagnostic messages | **Required for Deep Mode** |
| `./workflows/03-icp-scoring/` | ICP definition, segments, pain points | Optional - enriches angle targeting |
| `./workflows/11-performance-analysis/` | Past campaign performance, known angles | Optional - avoids repeating tested angles |

### Feeds Into (Downstream)

| Skill | How It Uses Creative GTM Output |
|-------|-------------------------------|
| Campaign creation | Builds full campaign from an ALPHA angle |
| Copywriting | Generates email sequences from message frameworks |
| Content workflows | Converts INTERESTING angles to thought leadership |
| Segment launch | Launches test batches for ALPHA angles |
| Standard campaign ideation | Absorbs proven angles into the 90% playbook after testing |

### Lifecycle

```
situation-mine -> creative-gtm deep -> test ALPHA angles -> performance-analysis
                                                                    |
                                                        angle proven? -> campaign ideation (absorb)
                                                        angle failed? -> discard, learn, iterate
```

---

## Examples

### Example 1: Quick Mode
```
User: /creative-gtm examplecoffee.com

Claude: Running Quick Mode for examplecoffee.com...

[5 Serper searches in parallel]
[Extracts 3 signal clusters: Instagram visual presence + no e-commerce,
 permit/licensing requirements, tariff exposure on imported goods]
[Applies 5 forcing functions per cluster]
[Generates 4 angles, scores each]

Output:
- ALPHA (8.3): Instagram cup detection -> permit cross-reference outbound
- PROMISING (7.1): Tariff wedge messaging for Q2 import season
- INTERESTING (5.2): Seasonal timing content piece -> redirect to content
- COMMODITY (3.1): "We help food service companies" -> discard, use standard ideation
```

### Example 2: Deep Mode
```
User: /situation-mine examplecoffee.com
[situation-mine runs, outputs worldview data]

User: /creative-gtm deep examplecoffee.com

Claude: Running Deep Mode for examplecoffee.com...
  Situation-mine data found (2 days old)

[7 additional Serper searches]
[Worldview conflict analysis: "family-owned values" vs rapid expansion signals]
[Cross-references hidden-signals-library for Food Service patterns]
[Generates 6 angles]

Output includes worldview conflicts, richer signal clusters,
shelf life warnings on all ALPHA/PROMISING angles
```

### Example 3: Missing prerequisite
```
User: /creative-gtm deep newprospect.com

Claude: No situation-mine output found for newprospect.com.
Deep Mode requires prospect worldview data.
Run `/situation-mine newprospect.com` first, then come back
with `/creative-gtm deep newprospect.com`.
```

### Example 4: Content output
```
User: /creative-gtm examplecoffee.com
[generates angles, one scores INTERESTING at 5.4]

Claude: ...
## INTERESTING (4.0-5.9) - Redirect to Content

### Angle 3: Permit Scraping as Competitive Intelligence

Score: 5.4 - **INTERESTING**

Content redirect: This angle works better as thought leadership.
-> Platform: LinkedIn
-> Hook: "Your competitors' new locations are public record.
   Here's how to find them before they announce."
```

---

## Related

- `./workflows/05-situation-mining/` - Prospect worldview research (required upstream for Deep Mode)
- `./workflows/07-message-market-fit/` - Systematic message-market fit testing
- `./workflows/11-performance-analysis/` - Measure actual alpha after testing angles
- `./workflows/10-campaign-launch/` - Launch test batches at scale
