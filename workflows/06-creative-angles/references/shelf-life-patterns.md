# Shelf Life Patterns

Every creative angle has a decay curve. The moment a competitor discovers the same angle, the alpha disappears. This reference defines decay categories, estimation methodology, and refresh triggers.

---

## Decay Categories

| Category | Typical Shelf Life | What Drives Decay | Examples |
|----------|-------------------|-------------------|---------|
| **Regulatory / Deadline** | Until date passes | The deadline itself -- once it passes, the urgency evaporates | CMS reimbursement changes, tariff effective dates, compliance deadlines, permit expirations |
| **Competitive Move** | 1-3 months | News cycle -- competitors react, market adjusts, the "news" becomes common knowledge | Competitor funding round, product launch, leadership change, market entry |
| **Data Insight** | 3-6 months | Discovery by others -- conference talks, blog posts, Clay templates, LinkedIn thought leaders | OSHA pattern analysis, review sentiment trends, tech stack correlations, hiring pattern inference |
| **Industry Pattern** | 6-12 months | Slow diffusion -- takes time for the pattern to become conventional wisdom | Seasonal demand cycles, vendor contract renewal patterns, budget cycle timing |
| **Structural** | 12+ months | Fundamental shifts -- requires industry restructuring, regulatory change, or technology disruption to become common | Ecosystem gaps between tools, cross-industry mechanism transfers, identity-level worldview conflicts |

---

## Estimation Method

Count the **research steps** a competitor would need to independently discover the angle:

| Research Steps Required | Estimated Shelf Life | Reasoning |
|------------------------|---------------------|-----------|
| 1 step (single Google search) | <1 month | Anyone doing basic research will find this. Not an angle -- it's common knowledge. |
| 2 steps (search + cross-reference) | 1-3 months | Slightly hidden but discoverable with moderate effort. |
| 3 steps (multiple sources, inference required) | 3-6 months | Requires connecting dots across sources. Most competitors won't bother. |
| 4+ steps (deep research, domain expertise, lateral thinking) | 6-12+ months | Requires both effort AND insight. This is where real alpha lives. |

**What counts as a "step":**
- One distinct data source consulted (e.g., checking OSHA database = 1 step)
- One inference drawn from data (e.g., OSHA citations + hiring pattern = quality problem = 1 step)
- One cross-reference between sources (e.g., OSHA data x job postings x Google Reviews = 1 step)

**Example estimation:**

```
Angle: Instagram cup detection -> permit cross-reference -> first-mover supply pitch

Steps for competitor to discover:
1. Notice prospect's Instagram presence (obvious) -- 1 step
2. Realize cups in Instagram photos reveal brand preferences (non-obvious) -- 1 step
3. Cross-reference with food service permit database (domain knowledge) -- 1 step
4. Combine permit data with supply chain timing (lateral thinking) -- 1 step
5. Build the outreach sequence around this specific chain (execution) -- 1 step

Total: 5 steps -> Estimated shelf life: 6-12 months
```

---

## Cross-Check: Is the Alpha Already Gone?

Before assigning shelf life, check if the angle has already been commoditized:

| Check | How to Check | If Found |
|-------|-------------|----------|
| **Clay Templates** | Search Clay's template library for similar approaches | Alpha is gone -- shelf life = 0. Use proven campaign patterns instead. |
| **LinkedIn Thought Leaders** | Search `"{angle keyword}" site:linkedin.com` | Alpha is weakening -- reduce shelf life by 50%. |
| **Conference Talks** | Search `"{angle keyword}" conference OR summit OR inbound` | Alpha is diffusing -- reduce shelf life by 30%. |
| **Blog Posts / Guides** | Search `"{angle keyword}" how to OR guide OR playbook` | Alpha is commoditizing -- reduce shelf life by 40%. |
| **Competitor Outreach** | Ask prospects: "Have you gotten emails like this before?" | If yes, alpha is gone for this specific prospect (may still work on others). |

**Rule:** If an angle appears in ANY Clay template, it is no longer creative GTM. It's proven GTM. Use proven campaign patterns instead.

---

## Shelf Life by Angle Type

| Angle Type | Base Shelf Life | Modifiers |
|------------|----------------|-----------|
| Regulatory/compliance deadline angle | Until deadline + 30 days | Longer if post-deadline consequences persist |
| Competitor intelligence angle | 1-3 months | Shorter if competitor is high-profile, longer if niche |
| Hiring pattern inference | 3-6 months | Shorter if the company is well-known, longer if private |
| Tech stack gap analysis | 3-6 months | Longer if the gap requires domain expertise to spot |
| Cross-industry transfer | 6-12 months | Longer if source industry is unrelated to prospect's industry |
| Review/sentiment mining | 3-6 months | Shorter if reviews are on popular platforms (G2, Trustpilot) |
| Public record analysis (permits, OSHA, etc.) | 6-12 months | Longer if the data source is niche, shorter if well-known |
| Worldview conflict angle | 6-12 months | Longest shelf life -- requires both research AND interpretation |
| Seasonal timing play | Seasonal (recurring) | Resets each cycle, but competitors may adopt after 1-2 cycles |

---

## Refresh Triggers

### Scheduled Refresh
- **Every 90 days:** Re-evaluate all active angles. Check cross-check sources for commoditization.
- **When shelf life expires:** Either refresh the angle with new data or retire it.
- **Quarterly industry scan:** Check for new regulations, market shifts, and competitive moves.

### Event-Driven Refresh
- **Industry regulation change:** Any new regulation in the prospect's industry invalidates regulatory angles and may create new ones.
- **Prospect major event:** Funding round, acquisition, leadership change, product launch -- all require re-evaluation.
- **Competitor copies the angle:** If you see a competitor using a similar approach, shelf life drops to 0 for that specific angle.
- **Conference season:** After major industry conferences (INBOUND, SaaStr, Dreamforce, etc.), check if any angles were discussed from stage.
- **Clay template update:** When Clay releases new templates, check if any match your active angles.

### Refresh Process

```
1. Pull the original angle and its signal cluster
2. Re-run the relevant searches
3. Check: Are the original data points still valid?
4. Check: Have new data points emerged that strengthen or weaken the angle?
5. Run the cross-check (Clay templates, LinkedIn, conferences, blogs)
6. Re-score using Asymmetry Score
7. Decision:
   - Score improved -> Extend shelf life, continue testing
   - Score unchanged -> Continue as-is
   - Score declined -> Retire angle, archive learnings
   - Score dropped below 4.0 -> COMMODITY. Move to proven patterns if validated, discard if not.
```

---

## Documenting Shelf Life in Output

Every ALPHA and PROMISING angle should include:

```markdown
Shelf Life: {estimate} -- {category}
Research steps to discover: {N} ({brief description of steps})
Decay trigger: {what specific event would kill this angle}
Cross-check: {Clay templates: N, LinkedIn posts: N, Conference talks: N}
Next refresh: {date, 90 days from generation or shelf life expiry, whichever is sooner}
```

**Example:**

```markdown
Shelf Life: 6-9 months -- Data Insight (public record analysis)
Research steps to discover: 4 (Instagram analysis -> brand detection -> permit cross-reference -> supply timing)
Decay trigger: A Clay template for "food service permit monitoring" or a viral LinkedIn post about this approach
Cross-check: Clay templates: N, LinkedIn posts: N, Conference talks: N
Next refresh: {date + 90 days}
```
