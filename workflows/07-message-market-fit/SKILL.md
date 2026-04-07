---
name: message-market-fit
description: Systematic message-market fit testing engine. Maps markets via MSPA, designs experiment batches, interprets results, makes scale/iterate/kill decisions. USE WHEN user says "message-market-fit" OR "mmf" OR "test messaging" OR "message fit" OR "test angles" OR "which message works" OR "experiment design" OR "potency test" OR "test campaigns" OR "what resonates" OR wants to systematically test outbound messaging.
---

# Message-Market Fit Testing Engine

Systematic experimentation framework for finding what resonates. Based on Kellen Casebeer's methodology: segment granularly, test with conviction, let results dictate next moves.

**Philosophy:** Outbound is a truth system. Every message is a hypothesis. Responses are data. Silence is data. The things that work and the things you wanted to work are not synonymous.

## When to Use This Skill

- Testing new messaging for a market you haven't cracked yet (uphill pipeline)
- Entering a new vertical or persona with no proven playbook
- Current campaigns are flat and you need to find what resonates
- Designing the first batch of experiments for a new client
- Deciding what to test next after initial results come back
- Evaluating whether a market is worth continued investment

## Core Framework: MSPA

Every campaign maps to exactly one cell in this matrix:

|Layer|What It Is|How to Think About It|
|-----|----------|---------------------|
|**Market**|Familiar grouping of companies|What the average SDR would say: "series B SaaS", "trucking companies", "waste haulers"|
|**Segment**|Meaningful division that changes communication|How do THEY think of themselves? Product-led vs sales-led. Independent vs franchise. Urban vs rural.|
|**Persona**|The CEO of the problem inside the company|Same title in different segments = different person. CMO at product-led vs CMO at sales-led.|
|**Angle**|YOUR directional argument AT them|Different from pain (static, prospect-owned). Angle is your argument to make. "PE is coming for your contracts" vs "Your drivers are your brand".|

**Critical insight:** The way you divide the TAM dictates the messaging you can do. Data strategy and messaging strategy must be co-developed. You cannot write great messages for bad segments.

## Modes

### Mode 1: MAP (New Market Entry)

For markets with no existing campaign data. Produces the MSPA matrix and first experiment batch.

### Mode 2: ITERATE (Post-Results)

Feed in campaign results. Interprets qualitatively, decides next experiments.

### Mode 3: DIAGNOSE (Stuck Pipeline)

For markets where you're sending but not getting traction. Identifies whether the problem is market, segment, persona, or angle.

---

## Mode 1: MAP

### Step 1: Pipeline Environment Check

Before mapping, classify the environment:

**Downhill Pipeline** - Product-market fit exists. Prospects already want this category of thing. They're shopping or would shop if nudged. You just need to tell them you exist with the right framing.
- Signal: Competitors running volume outbound. Category terms get searched. Active buying community.
- Action: Less experimentation needed. Focus on segment/angle optimization, not validation.

**Uphill Pipeline** - No established demand. Prospects aren't thinking about this. You need to find what argument makes them care enough to take a meeting.
- Signal: No one else cold emailing this market. No category search volume. Prospects don't know they need this.
- Action: Heavy experimentation. Wide MSPA map. Expect asymmetric results - most tests will fail, but the ones that hit will hit hard.

**Ask the user:** "Is this market downhill (they know they need this category) or uphill (we need to make them care)?"

### Step 2: Three-Lens Market Analysis

Apply three lenses to generate the MSPA matrix. Each lens reveals different segments.

**Lens 1: Customer's Worldview**
Read existing client context (`learnings.md`, `context.md`, intake notes). Extract:
- How does the client describe their market? (This is biased but deep)
- What language do they use?
- Where have they sold before? Where did it work vs not?
- Apply "healthy friction" - don't accept their first answer. "Series A finance teams" is too high-level. Push deeper.

**Lens 2: Fresh Research**
Run Serper searches on the market. Look for:
- How does this market naturally cluster? What communities, events, tools, identities exist?
- What's the internal dialogue of this persona? What are they reading, discussing, worried about?
- What are the tribal identities? (Not demographics - cultural/linguistic groups)
- What would make someone in this market say "this person gets me" vs "this is spam"?

**Lens 3: Data-Driven Segmentation**
Look at what's actually sourceable and filterable:
- What data points can we actually segment on? (Tech stack, funding stage, headcount, geography, hiring signals, tool usage)
- Which of these segments create messaging opportunities? (A segment that doesn't change what you'd say is useless)
- What's the intersection of "interesting segment" and "we can actually build this list"?

### Step 3: Generate MSPA Matrix

Output a matrix with this format:

```
## MSPA Matrix: [Client/Product]
Pipeline Environment: [Uphill/Downhill]

### Markets
1. [Market 1] - [Est. TAM size] - [Why this market]
2. [Market 2] - [Est. TAM size] - [Why this market]

### Segments per Market
Market 1:
  - Segment A: [Description] | [How it changes messaging] | [Data sourceable: Y/N]
  - Segment B: [Description] | [How it changes messaging] | [Data sourceable: Y/N]

### Personas per Segment
Market 1 > Segment A:
  - Persona X: [Title/role] | [What they care about in THIS segment] | [How they differ from same title in other segments]

### Angles per Persona
Market 1 > Segment A > Persona X:
  - Angle 1: [The argument] | [Why it might resonate] | [Confidence: HIGH/MED/LOW]
  - Angle 2: [The argument] | [Why it might resonate] | [Confidence: HIGH/MED/LOW]
```

**Segment quality check:** For each segment, ask: "If I removed our product from the equation, would these people still cluster this way? Do they think of themselves this way?" If yes, it's a real segment. If no, it's a product-centric filter masquerading as a segment.

**Angle quality check:** An angle is NOT a pain point. Pain is static and prospect-owned ("our costs are high"). An angle is your directional argument ("PE firms are acquiring your competitors at 8x EBITDA because they automated route optimization - you're leaving money on the table"). Angles have a point of view. They make a claim. They create tension.

### Step 4: Design Experiment Batch

Select the first 5 experiments from the matrix. Criteria for selection:

1. **Spread across segments** - Don't test 5 angles to the same segment. Test breadth first.
2. **Include at least one low-confidence "yolo" test** - The asymmetric winners come from unexpected places
3. **Prioritize sourceable segments** - No point testing a segment you can't build a list for
4. **Include one "obvious" test** - The thing you'd bet on. This is your control.

Output format:

```
## Experiment Batch 1

| # | Market | Segment | Persona | Angle | Contacts | Confidence |
|---|--------|---------|---------|-------|----------|------------|
| 1 | [M]    | [S]     | [P]     | [A]   | 600      | HIGH       |
| 2 | [M]    | [S]     | [P]     | [A]   | 600      | MED        |
| 3 | [M]    | [S]     | [P]     | [A]   | 600      | LOW        |
| 4 | [M]    | [S]     | [P]     | [A]   | 600      | MED        |
| 5 | [M]    | [S]     | [P]     | [A]   | 600      | YOLO       |

Total: 3,000 contacts across 5 experiments
Emails per experiment: 2-step sequence
Timeline: 2-3 weeks to first reads
```

### Step 5: Write Hypothesis Cards

For each experiment, write a hypothesis card:

```
### Experiment [N]: [Market] > [Segment] > [Persona] > [Angle]

Hypothesis: [Persona] in [Segment] will respond to [Angle] because [reasoning].

What "works" looks like:
- Reply rate > 3% = signal worth investigating
- Reply rate > 5% = strong signal, expand
- Meeting rate > 1% = asymmetric, scale immediately
- Interested replies (not just "remove me") = message resonates

What we'll learn even if it fails:
- [What silence or negative replies would tell us]

List build notes:
- [How to source this segment - what filters, what tools]
- [Expected list size]
- [Any data enrichment needed]
```

### Step 6: Barbell Allocation

Apply barbell theory to the full sending volume:

```
## Barbell Allocation

SAFE SIDE (80% of total volume):
- [Proven campaigns / existing winners / known-good segments]
- Purpose: Revenue. Pipeline. Keep the lights on.

EXPERIMENT SIDE (20% of total volume):
- Batch 1: [The 5 experiments above]
- Purpose: Discovery. Find the next asymmetric winner.

Rule: NEVER stop the experiment side. Even when safe side is crushing it.
When safe side struggles, INCREASE experiment side (you need new winners faster).
```

---

## Mode 2: ITERATE

### Input Required
- Campaign results (reply rates, meeting rates, interested count)
- Reply content (even 3-5 representative replies reveal everything)
- Which experiments from the batch

### Step 1: Classify Each Experiment

For each experiment, classify into one of three buckets:

**SUPER WORKS (Scale)**
- Meeting rate > 1% OR reply rate > 5% with quality replies
- Action: Expand volume. Same segment + angle, bigger list. Consider adjacent segments.
- Don't touch the messaging. Scale what's working, don't optimize a winner.

**KIND OF WORKS (Iterate)**
- Reply rate 2-5% OR some interested replies but not converting to meetings
- Action: The segment might be right but the angle needs sharpening. Or the angle is right but the segment is too broad. Split test:
  - Same segment, different angle
  - Same angle, tighter segment
  - Same everything, different persona

**DOESN'T WORK (Kill or Channel-Switch)**
- Reply rate < 1% OR all replies are "not interested" / "remove me"
- Action: Before killing entirely, check:
  - Was the list quality good? (Bad data = bad results regardless of message)
  - Was deliverability healthy? (Check bounce rates, spam complaints)
  - If both were fine: the concept doesn't resonate in email. Consider: would this work as a cold call? LinkedIn? Content play?
  - If neither worked: move to next segment. This one's dead.

### Step 2: Read the Replies

This is the most underrated step. Read every reply, not just the interested ones.

**What to extract from replies:**
- **Language they use** - Do they describe the problem the same way you did? If not, their language is better than yours. Use it.
- **Objections** - These are segment signals. "We already have this" = wrong segment. "We're too small for this" = wrong segment. "This is interesting but timing is bad" = right segment, need trigger event.
- **Emotional tone** - Annoyed = irrelevant message. Curious = right direction. Excited = you found something.
- **Questions they ask** - If they ask "how does this work?" you have a message problem (not clear). If they ask "what would this cost?" you have a winner.

### Step 3: Design Next Batch

Based on classifications, generate Experiment Batch N+1:

```
## Experiment Batch [N+1]

Based on Batch [N] results:
- Scaling: [Experiment X] - expanding from 600 to [2,000-5,000] contacts
- Iterating: [Experiment Y] - same segment, new angle: [describe]
- Iterating: [Experiment Z] - same angle, tighter segment: [describe]
- New test: [Fresh experiment from MSPA matrix]
- Yolo: [Wild card test based on something unexpected from replies]
```

### Step 4: Update MSPA Matrix

After each batch, update the matrix with results:

```
### Angle Results Log
| Experiment | M > S > P > A | Contacts | Reply% | Meeting% | Verdict |
|------------|---------------|----------|--------|----------|---------|
| B1-E1      | [...]         | 600      | 6.2%   | 1.8%     | SCALE   |
| B1-E2      | [...]         | 600      | 1.1%   | 0%       | KILL    |
| B1-E3      | [...]         | 600      | 3.4%   | 0.5%     | ITERATE |
```

Mark tested angles on the matrix. Cross off dead segments. Circle winners. The matrix becomes a map of what you know about this market.

---

## Mode 3: DIAGNOSE

For when campaigns are running but results are flat across the board.

### Diagnostic Sequence

Work through these in order. The first one that's broken is the one to fix.

**1. Is the MARKET wrong?**
- Are these companies actually buying things like this? Do competitors sell to them?
- Is this a downhill or uphill environment? If uphill, flat results might be expected - you need more experiments, not more volume.
- Check: Look at competitor customer pages. If no one sells to this market, you might be pioneering (hard) or delusional (common).

**2. Is the SEGMENT wrong?**
- Are you segmenting on something that actually changes messaging? Or just filtering by size/geography without changing what you say?
- Test: Take your current message and mentally send it to a different segment. If it reads exactly the same, your segmentation isn't working.
- The fix: Segment by identity (how they see themselves), not demographics (how a database sees them).

**3. Is the PERSONA wrong?**
- Are you reaching the CEO of the problem? Or someone adjacent who can't make the decision?
- Are you reaching someone who feels the pain, or someone who manages the budget?
- Test: Read your replies. If people say "interesting, let me forward this to X" - you're at the wrong persona. Go to X.

**4. Is the ANGLE wrong?**
- Are you leading with what you do (product pitch) instead of a directional argument (angle)?
- Does your angle create tension? Does it make a claim? Does it have a point of view?
- Test: Read your email. If you could swap your company name for any competitor and it still reads the same, your angle is generic.

**5. Is it EXECUTION (not strategy)?**
- List quality (bad emails, wrong contacts)
- Deliverability (landing in spam)
- Timing (holiday, end of quarter, budget freeze)
- Volume (sample too small to read signal)

### Diagnostic Output

```
## Diagnosis: [Client/Campaign]

Campaigns analyzed: [list]
Total sent: [N] | Reply rate: [%] | Meeting rate: [%]

Root cause: [MARKET / SEGMENT / PERSONA / ANGLE / EXECUTION]

Evidence:
- [What the data shows]
- [What the replies tell us]
- [What the silence tells us]

Prescription:
- [Specific next action]
- [What to change]
- [What to keep the same]
```

---

## Key Principles (Kellen's Laws)

1. **Resonance beats personalization.** If the only way you can connect with your market is 1:1 research per person, you don't understand the market well enough. Find the minimum division that still feels deeply personal.

2. **Identity beats information.** Showing you understand what makes them unique > telling them what you do. "I saw you're hiring cobalt programmers" > "I help companies with software development."

3. **Groups are cultural, not demographic.** People who attend Smart Lead office hours are a tribe. "Tech companies with 50-200 employees" is a database filter. One creates messaging opportunities. The other doesn't.

4. **The things that work and the things you wanted to work are not synonymous.** Run the experiments. Let the results dictate. Your intuition is the starting point, not the answer.

5. **Silence is data.** A campaign with 0.5% reply rate is telling you something just as clearly as one with 5%. The absence of response IS the response.

6. **Never stop the experiment side.** Barbell theory - 80% volume on what's working, 20% on experiments. Winners decay. You always need the next one in the pipeline.

7. **Qualitative > quantitative for early-stage testing.** You don't need statistical significance with 600 contacts. You need to read the replies and feel whether the market is leaning toward you or away from you. 10 thoughtful replies tell you more than 10,000 emails' worth of open rate data.

8. **Wrong and specific is worse than wrong and general.** If AI-generated personalization gets a fact wrong and it's specific ("I saw you raised $5M last month" when they didn't), that's devastating. If it's general ("sounds like you're growing fast"), nobody cares. Design for graceful failure.

9. **The best campaigns look nothing like what you planned.** The 16-meetings-from-300-emails campaign came from a "yolo, we're about to lose this client" experiment. Stay in motion. The asymmetric winners come from unexpected places.

10. **Outbound is how we discover, validate, and invalidate hypotheses.** We don't need better tools. We need better hypotheses. Outbound is the fastest way to test them.

---

## Integration with Other Skills

|Skill|Relationship|
|-----|------------|
|`./workflows/06-creative-angles/`|Feeds ANGLES into the MSPA matrix. Run creative-gtm first to discover hidden signal angles, then test them here.|
|`./workflows/04-gtm-strategy/`|Produces the initial market research and persona profiles. MMF takes those and turns them into experiment design.|
|Campaign creation|Executes the experiments. Each experiment = one campaign creation workflow.|
|`./workflows/11-performance-analysis/`|Reads the results. Feed analysis output back into Mode 2: ITERATE.|
|`./workflows/12-campaign-debrief/`|Captures the learnings. Debriefs update the MSPA matrix and intelligence layer.|
|Intelligence query|Check what's already known before designing experiments. Don't re-test what's already proven.|
|`./workflows/10-campaign-launch/`|Launches the batch. 5 experiments = 5 parallel segment-launches.|
|Reply analysis|Deep analysis of reply content for Step 2 of ITERATE mode.|

### Recommended Workflow

```
Intelligence query              <- What do we already know?
./workflows/06-creative-angles/ <- Discover hidden signal angles
./workflows/07-message-market-fit/ MAP  <- Build MSPA matrix + first batch
Campaign creation               <- Build campaigns (x5)
./workflows/10-campaign-launch/ <- Launch batch
[wait 2-3 weeks]
./workflows/11-performance-analysis/ <- Read results
Reply analysis                  <- Deep dive on replies
./workflows/07-message-market-fit/ ITERATE <- Design next batch
./workflows/12-campaign-debrief/    <- Capture learnings to intelligence
[repeat]
```

---

## Output Files

Save all MMF work to the client's knowledge folder:

- `./clients/{client}/mmf-matrix.md` - The living MSPA matrix
- `./clients/{client}/mmf-batch-{N}.md` - Each experiment batch design
- `./clients/{client}/mmf-results-{N}.md` - Results interpretation per batch

---

## Examples

### Example 1: New Client, Uphill Market

User: "mmf map for Acme Field Services - they sell field service management software to blue-collar businesses"

Output: Pipeline environment check (uphill - waste/HVAC/plumbing companies aren't shopping for FSM software), three-lens analysis, MSPA matrix with markets (waste haulers, HVAC companies, plumbing companies, electrical contractors), segments per market (independent vs franchise, <50 trucks vs 50+, urban vs rural), personas (Owner/GM, Operations Manager, Dispatch Lead), angles per persona, first batch of 5 experiments, hypothesis cards, barbell allocation.

### Example 2: Post-Results Iteration

User: "mmf iterate - here are the results from batch 1 for the waste management campaign"

Output: Classify each experiment (scale/iterate/kill), read replies qualitatively, extract language and objections, update MSPA matrix with results, design batch 2 with expansions of winners and iterations on promising signals.

### Example 3: Stuck Pipeline

User: "mmf diagnose - we've sent 5,000 emails to SaaS CTOs and reply rate is 0.8% across all campaigns"

Output: Run diagnostic sequence (market > segment > persona > angle > execution), identify root cause with evidence, prescribe specific next action.
