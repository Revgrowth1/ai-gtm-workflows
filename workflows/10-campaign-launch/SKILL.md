---
name: campaign-launch
description: Full cold email campaign setup from CSV to sending. Validates, enriches with situation mining, segments by email host, uploads to email platform with custom variables.
---

# Campaign Launch

Takes enriched lead CSV -> parallel situation mining (Serper + LLM) -> upload to email platform with custom variables -> create campaign with 2-step sequence.

IMPORTANT: Segmentation by email provider is ON by default. Use `--no-segment` to disable.

## CLI

```bash
python3 ./workflows/10-campaign-launch/launch.py ./leads.csv \
  -w {workspace} -c "Healthcare Compliance v1" --activate

# Key options
  --workspace / -w       # Required: email platform workspace
  --campaign / -c        # Campaign name (creates if provided)
  --template / -t        # Template: list-building, risk-reversal
  --region               # Region placeholder for template
  --niche                # Niche placeholder for template
  --variables / -v       # Comma-separated variable definitions
  --no-segment           # Disable email host segmentation
  --no-host-lookup       # Skip email host lookup
  --no-sequence          # Skip sequence creation
  --activate             # Activate after setup
  --preview              # Sample 3 companies
  --unique-per-lead      # Force unique vars per lead (auto for <500)
  --no-unique            # Disable per-lead uniqueness
  --reference            # Copy config from existing campaign ID
```

## Required CSV Columns

|Column|Required|
|---|---|
|email|Yes|
|first_name|Yes|
|company_domain|Yes|
|last_name, job_title, company_name|No|

## Email Platform Variable Format (CRITICAL)

IMPORTANT: ALL variables use `{VARIABLE_NAME}` - UPPERCASE, single curly braces. NEVER `{{variable}}`. NEVER lowercase.

### System Variables
`{FIRST_NAME}`, `{LAST_NAME}`, `{COMPANY}`, `{SENDER_FIRST_NAME}`, `{SENDER_LAST_NAME}`, `{SENDER_EMAIL}`

### Custom Variables
`{HOOK}`, `{SITUATION}`, `{EMAIL_PROVIDER}` (or any user-defined)

### Spintax
`{option1|option2|option3}` - use every 3-5 words for deliverability.

## Email Formatting Rules (CRITICAL)

1. Greeting merged with first sentence - NO separate "Hi Name," line
2. `<br><br>` between paragraphs - NOT `<p>` tags
3. Single `<br>` before sign-off: `{Best|Cheers},<br>{SENDER_FIRST_NAME}`

## API Patterns (CRITICAL - NEVER VIOLATE)

|Pattern|Wrong|Correct|
|---|---|---|
|Variables|`{{first_name}}`|`{FIRST_NAME}`|
|Max sequence steps|3+|**2 MAXIMUM**|
|Custom vars array|`{"key":"X"}`|`{"name":"X","value":"Y"}`|
|Sequence wait|`wait_days`|`wait_in_days`|
|Sequence email|`subject`|`email_subject`|
|First step wait|`0`|`1` (minimum)|
|Em-dashes|`--` (em-dash)|commas, periods, hyphens|

## API Flow (Order Matters)

1. Email host lookup -> tag leads with ESP
2. CREATE custom variables -> `POST /api/custom-variables`
3. UPLOAD leads with variables -> `POST /api/leads/create-or-update/multiple`
4. CREATE campaign -> `POST /api/campaigns`
5. ATTACH leads -> `POST /api/campaigns/{campaign_id}/leads/attach-leads`
6. ATTACH sender emails -> `POST /api/campaigns/{campaign_id}/attach-sender-emails` (PAGINATE!)
7. APPLY schedule -> `POST /api/campaigns/{campaign_id}/create-schedule-from-template`
8. CREATE sequence -> `POST /api/campaigns/{campaign_id}/sequence-steps`
9. ACTIVATE (optional) -> `PATCH /api/campaigns/{campaign_id}/resume`

## Sender Emails (CRITICAL - ALWAYS PAGINATE, NEVER SPLIT)

**ALL sender emails attach to EVERY campaign. Never split/chunk senders across campaigns.**

The script verifies after attachment that the count matches. If verification fails, it warns and you must check manually.

```python
all_senders, page = [], 1
while True:
    data = api_get(f"sender-emails?per_page=100&page={page}")
    senders = data.get("data", [])
    if not senders: break
    all_senders.extend(senders)
    if page >= data.get("meta", {}).get("last_page", 1): break
    page += 1
connected_ids = [s["id"] for s in all_senders if s.get("status", "").lower() == "connected"]
# Attach ALL connected_ids to each campaign - never subset
```

## Pre-Launch Validation

1. **Variable Check**: Extract all `{VARIABLE}` from copy, verify lead fields populated
2. **Messaging Sanity**: Value first? Specific outcome? Risk reversal? Social proof? Clear CTA? Spintax balanced?
3. **Lead Spot Check**: Sample 3-5 leads to verify data
4. **Preview Email**: Use platform preview before activating

## Email Host Segmentation (Default)

Auto-creates campaigns per provider: `"Campaign | Google"`, `"Campaign | Microsoft"`, `"Campaign | Other"`.

|Host Lookup Result|Segment|
|---|---|
|Google|Google|
|Outlook|Microsoft|
|Proofpoint, Mimecast, Barracuda, Cisco, Custom, Unknown|Other|

## Unique Per-Lead (Auto for <500)

Each lead gets unique variables based on role + company context using Josh Braun framework (fear of loss > gain, demonstrate research, humble tone, specificity).

## Campaign Templates

### `list-building`
Best for owner/CEO targets, 11-50 employees, industrial niches. Tier 2 (Free Asset).

Naming: `{Niche} | Owners | {Source} | {Region} | 11-50 | List Building Offer`

Settings: `{"type":"outbound","plain_text":true,"open_tracking":false,"can_unsubscribe":false,"include_auto_replies_in_stats":true,"max_emails_per_day":1000,"max_new_leads_per_day":1000}`

Schedule: Mon-Fri, 08:00-17:00 local time

Step 1 (Day 1):
```
Subject: {Quick question|Question|Thought} for {FIRST_NAME}
Body: <p>{FIRST_NAME} - {Got|Put together|Have} a list of {companies|businesses} actively {buying|purchasing|sourcing} {NICHE} in the {REGION}.</p><p><br></p><p>{Worth sending|Want me to send|Mind if I send} a sample for {COMPANY} to {look at|review|check out}?</p><p><br></p><p>{SENDER_FIRST_NAME} - [Your Agency]</p>
```

Step 2 (Day 3):
```
Subject: Re: {Quick question|Question|Thought} for {FIRST_NAME}
Body: <p>{FIRST_NAME} - {floating this back up|circling back|following up}.</p><p><br></p><p>{Happy to send|Can send|Glad to share} that prospect sample if {useful|helpful|of interest}.</p><p><br></p><p>{If not, no worries|No pressure either way|All good if not}.</p><p><br></p><p>{SENDER_FIRST_NAME} - [Your Agency]</p>
```

No custom lead variables needed - system variables only.

### `risk-reversal`
Tier 4 (Risk Reversal). Best for higher-touch, 51-200+ employees, or when list-building underperforms.

Naming: `{Niche} | {Target Title} | {Source} | {Region} | {Employee Count} | Risk Reversal Offer`

Step 1 (Day 1):
```
Subject: {outbound for {COMPANY}|done-for-you outbound|quick test}
Body: <p>{FIRST_NAME} - we {build|create} {done-for-you|fully managed} outbound systems.</p><p><br></p><p>{Here's the deal|The offer}: We'll {launch a campaign|run outbound} for {COMPANY} {at no cost|for free}. You {keep every lead|own all replies}. If {it works|you're happy}, we {talk next steps|discuss longer engagement}. If not, {you got free leads|no hard feelings}.</p><p><br></p><p>{Did this for|Built this for} [Example Client] - 150 replies, 11 opportunities.</p><p><br></p><p>{Worth a quick look|Open to a 15-min call}?</p><p><br></p><p>{SENDER_FIRST_NAME} - [Your Agency]</p>
```

Step 2 (Day 3):
```
Subject: Re: {outbound for {COMPANY}|done-for-you outbound|quick test}
Body: <p>{FIRST_NAME} - {floating this back up|circling back|following up}.</p><p><br></p><p>{If outbound|If scaling outbound} {isn't a priority|isn't top of mind} right now, {no worries|totally understand}.</p><p><br></p><p>{But if it is|If it's worth exploring}, {happy to show|can show} you {what we built|the system we built} for [Example Client].</p><p><br></p><p>{Either way|No pressure},<br>{SENDER_FIRST_NAME}</p>
```

### Adding Templates
Capture when campaign achieves >1% reply rate, >0.5% interested rate. Record ID, copy, settings. Identify fixed vs variable parts.

## Messaging Framework

### Value Equation (Hormozi)
`Value = (Dream Outcome x Perceived Likelihood) / (Time Delay x Effort/Sacrifice)`

### Offer Tiers

|Tier|Type|Conversion|
|---|---|---|
|1|Knowledge/Audit|Low|
|2|Free Asset|Medium|
|3|Done-For-You Trial|High|
|4|Risk Reversal|Highest|

### Offer Selection

|Client Type|Offer|
|---|---|
|Agency -> SMBs|Free ICP List + Framework|
|SaaS -> Enterprise|Done-For-You Trial|
|MedTech/Healthcare|Pilot Program|
|Internal Outbound|Risk Reversal (Pay-Per-Interested)|

### Before Writing Sequences
Gather from client: (1) What can they GIVE free? (2) Best case study with numbers? (3) What guarantee? (4) Time-to-value?

Adapt process: Read `./clients/{client}/context.md` -> identify strongest tier -> pull case study -> adapt templates -> test against checklist.

### Message Market Fit (Eric Nowoslawski)
Cold email = demand generation. Even demand-capture offers need demand-gen framing. Slant by messaging ("audit what your bookkeeper is doing" not "need bookkeeping?") and by list (narrow = demand gen).

**4-Phase Testing**: Phase 1 (direct sales) -> Phase 2 (feedback + skepticism) -> Phase 3 (offer testing) -> Phase 4 (lookalike campaigns). If running yourself, START WITH PHASE 4.

**Recency Waterfall** (better than generic personalization): New job > LinkedIn post > Company news > CEO podcast > Company post > Fallback ("Not sure if you or {COLLEAGUE} handles this").

**B2B = 3 things**: Make money, save money, save time. Subject lines: "Quick question", "Question for {FIRST_NAME}", "{COMPANY_NAME}".

### Offer Variables

|Variable|Purpose|
|---|---|
|`{OFFER_HOOK}`|Tangible deliverable|
|`{PROOF_POINT}`|Specific result|
|`{RISK_REVERSAL}`|Safety language|
|`{TIME_TO_VALUE}`|Speed promise|
|`{SIMILAR_COMPANY}`|Social proof|

## Workspace Configuration

Configure your email platform workspace API keys as environment variables:

```
EMAIL_PLATFORM_API_KEY=your_api_key_here
```

If you manage multiple workspaces (one per client), use a naming convention:

```
EMAIL_PLATFORM_{CLIENT}_API_KEY=your_api_key_here
```

## Lead Upload Format

```python
lead = {
    "email": "john@example.com", "first_name": "John", "last_name": "Doe",
    "company_name": "Acme Corp", "website": "acme.com", "job_title": "VP Sales",
    "custom_variables": [
        {"name": "SITUATION", "value": "Ecommerce-first GTM"},
        {"name": "HOOK", "value": "Your website does the selling..."},
        {"name": "EMAIL_PROVIDER", "value": "Google"}
    ]
}
```

## Error Handling

|Error|Action|
|---|---|
|Missing required columns|Exit with message|
|Serper rate limit (429)|Wait 3s, retry|
|LLM timeout|Fallback values|
|Email platform batch failure|Log failed, continue|
|Custom variable exists|Skip (not error)|
|No host lookup API key|Skip host lookup|
|No sender emails|Warn, continue|

## Configuration

Keys from `./.env`:
`EMAIL_PLATFORM_API_KEY`, `SERPER_API_KEY`, `LLM_API_KEY`, `EMAIL_HOST_LOOKUP_API_KEY` (optional)

Related: `./workflows/08-contact-discovery/` (find emails first), `./workflows/11-performance-analysis/` (post-launch)
