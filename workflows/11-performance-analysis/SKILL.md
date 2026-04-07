---
name: performance-analysis
description: Analyze cold email campaign performance using the 5 Variables framework. USE WHEN you need to analyze campaigns, review performance, understand what's working, or evaluate reply/interested rates.
---

# Campaign Performance Analysis

Scientific method applied to cold email campaigns. Isolate variables, measure outcomes, generate actionable recommendations.

## The 5 Core Variables

|Variable|Measures|Key Question|
|--------|--------|------------|
|**Offer**|Value proposition|Compelling? Solves real pain?|
|**Message**|Copy, subject, CTAs|Clear? Tone matches audience?|
|**Segment**|Who you target|Right ICP? Accurate titles?|
|**Infrastructure**|Email setup (Google/MS, domains, warmup)|Landing in inbox? Reputation?|
|**Timing**|Send times, cadence|When are opens/replies happening?|

## Analysis Phases

### Phase 1: Hypothesis
State expectations before analyzing (e.g., "Google infra should outperform Microsoft").

### Phase 2: Data Collection
Pull 7-14 day period from your email platform. Segment by workspace, campaign name, infrastructure type. Calculate: Reply Rate, Interested Rate, Bounce Rate.

### Phase 3: Analysis
Apply: **Pareto** (which 20% drive 80% of results?), **Statistical Significance** (min 500 sent, 7+ days; small samples = "TEST MORE"), **Cohort Analysis** (compare similar periods), **Attribution** (map results to 5 variables).

### Phase 4: Recommendations
Prioritize: **SCALE** proven winners -> **PAUSE** underperformers -> **TEST** promising signals -> **ITERATE** specific changes.

## Report Structure (6 Sections)

### 1. Quick Health Check

|Metric|Benchmarks|
|------|----------|
|Reply Rate|>1% Healthy, 0.5-1% Attention, <0.5% Critical|
|Interested Rate|>25% of replies = Healthy|
|Bounce Rate|<3% Healthy, 3-5% Attention, >5% Critical|

### 2. Segment Performance Ranking
Rank all campaigns by Interested Rate.

|Verdict|Criteria|
|-------|--------|
|TOP PERFORMER|Highest interested rate, 500+ sent|
|SCALE|>1% reply, >25% interested|
|TEST MORE|<500 sent, promising signals|
|MONITOR|Average, needs more data|
|UNDERPERFORM|<0.5% reply OR <10% interested with 1000+ sent|

### 3. Infrastructure Analysis
Compare Google vs Microsoft. Key: is there 2x+ difference? If so, shift volume to winner.

### 4. Reply Sentiment Analysis
High replies + low interested = wrong audience. Low replies + high interested = good targeting, need volume.

### 5. Attribution Analysis
For top/bottom performers, identify root cause mapped to 5 variables.

### 6. Next Iteration Recommendations
Prioritized action table: Priority, Action, Variable, Expected Impact, Effort.

## Repeatable Checklist
- Volume: 7+ days? 500+ per segment? External factors?
- Performance: >1% reply? >25% interested? Any 0% despite volume?
- Infrastructure: Google vs MS winner? Bounce spikes >5%? Domain issues?
- Attribution: What drives winners? What blocks losers? Apples-to-apples comparison?
- Next: What to scale/pause/test?

## Output Format
**Spreadsheet** (preferred): `[Client] Campaign Analysis - [Date]`, 6 sections, conditional formatting.
**Quick Summary** (Slack/chat): Winners/Losers with rates + verdicts, key insight, next actions.

## Post-Analysis: Capture Learnings

**After completing the analysis, always suggest the debrief step:**

> Analysis complete. To capture these learnings so they compound into future campaigns, run the campaign debrief workflow.
>
> This will walk through a 5-question structured debrief and append findings to `learnings.md`.

The debrief is what closes the loop - without it, analysis insights evaporate into spreadsheets and chat. The debrief writes structured entries that feed:
- Campaign ideation - Pattern Match scoring for future campaigns
- Cross-client pattern recognition
- Monthly intelligence layer updates

## Integration Map

### Reads From
| Source | What It Provides |
|-------|-----------------|
| Email platform API | Raw campaign data (sent, replies, interested, bounces) |
| Client `context.md` | Campaign strategy, ICP for attribution context |

### Feeds Into
| Destination | How It Uses Analysis Output |
|-------|---------------------------|
| `./workflows/12-campaign-debrief/` | Analysis results flow directly into structured learning capture |
| Campaign ideation | Verdicts (SCALE/PAUSE/TEST) inform next campaign ideas |
| Campaign creation | Recommendations guide next iteration setup |
