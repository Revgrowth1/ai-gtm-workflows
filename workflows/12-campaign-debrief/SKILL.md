---
name: campaign-debrief
description: Structured post-campaign learning capture that compounds intelligence over time. USE WHEN you need to capture learnings, run a campaign retrospective, or log campaign results for a client.
---

# Campaign Debrief

Structured 5-question learning capture that closes the loop between campaign execution and campaign intelligence. Every debrief appends to the client's `learnings.md` and flags transferable insights for the cross-client intelligence layer.

**This is the keystone of the intelligence engine.** If debriefs don't happen, nothing compounds.

## When to Use

- After performance analysis completes (you'll be prompted)
- Standalone: run debrief for any campaign with results
- Retroactively: capture learnings from past campaigns that were never debriefed

## Workflow

### Step 1 - Load Context

Read from `./clients/{client}/`:

| File | What It Provides | Required? |
|------|-----------------|-----------|
| `learnings.md` | Existing learnings to append to | **Yes** (create from template if missing) |
| `context.md` | Campaign strategy, ICP, active campaigns | Recommended |
| `profile.md` | Verticals, personas, product info for tagging | Recommended |

If `learnings.md` doesn't exist, create it from the template structure (see Output Format below).

### Step 2 - Identify the Campaign

Ask or confirm:

```
Which campaign are we debriefing?

Campaign name: {name}
Client: {client}
Date range: {start} - {end}
```

**Data sources (try in order):**
1. If analysis was just completed - use those results directly
2. Pull from email platform API if workspace is known
3. Accept manual input from the user (sent count, reply rate, interested rate, meetings)

Display a quick stats summary before proceeding:

```
## Campaign Stats: {name}

| Metric | Value |
|--------|-------|
| Sent | {n} |
| Reply Rate | {x}% |
| Interested Rate | {y}% |
| E2L Ratio | 1:{n} |
| Meetings Booked | {n} |
| Bounce Rate | {z}% |
```

### Step 3 - 5-Question Debrief

Walk through each question. For each, offer a suggested answer based on available data and let the user confirm or override.

**Q1: What hypothesis did we test?**
> What did we expect to happen and why? What variable(s) were we testing?
>
> *Format: "We hypothesized that {angle/segment/timing} would {expected outcome} because {reasoning}."*

**Q2: What was the result?**
> Confirmed, partially confirmed, or rejected? One-line summary with the key metric.
>
> | Verdict | Criteria |
> |---------|----------|
> | **CONFIRMED** | Hypothesis validated - metrics met or exceeded expectations |
> | **PARTIAL** | Directionally correct but below threshold, or worked for subset only |
> | **REJECTED** | Hypothesis invalidated - metrics clearly below expectations |

**Q3: What worked and what didn't?**
> Separate the signal from the noise. What specific elements (angle, segment, timing, copy, infrastructure) drove results - positive and negative?

**Q4: What surprised us?**
> Unexpected findings - positive or negative. These are often the most valuable learnings.

**Q5: What's transferable?**
> Could this insight help another client? Is this vertical-specific, persona-specific, or a universal pattern?
>
> If yes -> tag it and flag for intelligence layer update.

### Step 4 - Determine Verdict

Based on the debrief, assign a campaign verdict:

| Verdict | Criteria | Next Action |
|---------|----------|-------------|
| **SCALE** | >1% reply, >25% interested, positive ROI signals | Increase volume, expand to similar segments |
| **ITERATE** | Promising signals but below threshold | Adjust one variable, re-test |
| **PAUSE** | Mixed results, unclear signal | Wait for more data or rethink approach |
| **KILL** | <0.5% reply with 500+ sent, or negative ROI | Stop this angle/segment, reallocate |

### Step 5 - Write the Entry

Append the structured entry to `./clients/{client}/learnings.md`.

**IMPORTANT:** Always append. Never overwrite existing entries.

### Step 6 - Tag and Flag

Apply tags from the entry:
- `#vertical/{vertical}` - e.g., `#vertical/saas`, `#vertical/healthcare`
- `#persona/{persona}` - e.g., `#persona/vp-engineering`, `#persona/cfo-finance`
- `#angle/{angle}` - e.g., `#angle/operational-efficiency`, `#angle/competitive-displacement`

If anything was marked transferable in Q5:
> **Transferable insight flagged.** Update the relevant intelligence file:
> - `intelligence/verticals/{vertical}.md`
> - `intelligence/personas/{persona}.md`
> - `intelligence/angles/{angle}.md`

---

## Debrief Entry Format

This is the exact format appended to `learnings.md`:

```markdown
---

### Campaign: {name} ({YYYY-MM-DD})
**Sent:** {n} | **Reply:** {x}% | **Interested:** {y}% | **E2L Ratio:** 1:{n} | **Meetings:** {n}
**Verdict:** SCALE / ITERATE / PAUSE / KILL

**Hypothesis:** {what we expected and why}
**Result:** {confirmed|partial|rejected} - {one-line summary}

**What Worked:**
- {angle/segment/timing} - {why it worked}

**What Didn't Work:**
- {angle/segment/timing} - {why it failed}

**Surprise:** {unexpected finding}
**Transferable:** {insight for other clients, or "None - client-specific"}
**Tags:** `#vertical/{v}` `#persona/{p}` `#angle/{a}`
```

## Learnings.md Template

If a client has no `learnings.md`, create one with this structure before appending:

```markdown
# Client Learnings: {Client Name}

> Cumulative learnings from all campaigns for this client.

---

## Summary Stats

| Metric | Value |
|--------|-------|
| Total Campaigns | 0 |
| Best Performer | N/A |
| Average Reply Rate | N/A |

---

## What Works

### Segments That Convert
- TBD

### Angles That Resonate
- TBD

---

## What Doesn't Work

### Segments to Avoid
- TBD

### Known Pitfalls
- TBD

---

## Campaign Log

*No campaigns logged yet*

---

## Notes

*Add ongoing observations and hypotheses to test*

---

*Last Updated: {month} {year}*
```

---

## Design Constraints

- **< 5 minutes to complete** - suggest answers from data, user confirms or overrides
- **Append-only** - never rewrite history in learnings.md
- **Tags are lowercase, hyphenated** - `#vertical/saas` not `#vertical/SaaS`
- **Verdicts are objective** - based on metrics and thresholds, not feelings
- **Data-first** - pull from email platform when possible, fall back to manual input

---

## Integration Map

### Reads From
| Source | What It Provides |
|-------|-----------------|
| `./workflows/11-performance-analysis/` | Analysis results, metrics, verdicts - direct handoff |
| Email platform API | Raw campaign data (sent, replies, interested counts) |
| Client `context.md` | Campaign strategy, ICP for tagging context |
| Client `profile.md` | Verticals, personas for tag assignment |

### Feeds Into
| Destination | How It Uses Debrief Output |
|-------|---------------------------|
| Campaign ideation | Reads `learnings.md` for Pattern Match scoring |
| Intelligence query | Transferable insights seed the cross-client intelligence layer |
| Intelligence synthesis | Monthly synthesis reads all debrief entries to update patterns |
| Campaign creation | Intelligence query surfaces relevant prior learnings |

---

## Examples

### Example 1: Post-analysis debrief
```
User: Run campaign debrief for Client C

Claude: Loading Client C context...
  > learnings.md - 10+ campaigns logged
  > context.md - Active campaigns found
  > profile.md - Data infrastructure vertical

Which campaign are we debriefing?
  Campaign name: Client C Google + Variant A v2
  Date range: 2025-11-15 - 2025-12-01

## Campaign Stats
| Metric | Value |
|--------|-------|
| Sent | 1,984 |
| Reply Rate | 5.7% |
| Interested Rate | 0.4% |
| E2L Ratio | 1:283 |
| Meetings | 3 |

[Walks through 5 questions with suggested answers from data]
[Appends entry to learnings.md]
[Tags: #vertical/data-infrastructure #persona/devops #angle/operational-efficiency]

Transferable insight flagged: Google infrastructure consistently
outperforms Microsoft across all segments (5.7% vs 0.4% reply).
This may apply to other clients - check intelligence/patterns.md.
```

### Example 2: Retroactive debrief (no prior analysis)
```
User: Run campaign debrief for Example Client

Claude: Loading Example Client context...
  > learnings.md - 8+ campaigns logged
  > context.md - Campaign focus found

Which campaign are we debriefing?
  [User provides: Campaign v1, manual stats]

[Walks through 5 questions]
[Appends entry to learnings.md]
```

---

## Related

- `./workflows/11-performance-analysis/` - Analyze performance (precedes debrief)
- Campaign ideation - Generate next campaign ideas (reads debrief output)
- Intelligence query - Query cross-client patterns
- Intelligence synthesis - Monthly pattern recognition across all debriefs
