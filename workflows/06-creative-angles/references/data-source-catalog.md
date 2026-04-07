# Data Source Catalog

Public and semi-public data sources for creative GTM angle research. Organized in 4 tiers by access complexity.

---

## Tier 1: Free, No Auth

Publicly accessible, no account needed. Start here.

| Source | What It Contains | How to Access | Best Industries | Automation Potential |
|--------|-----------------|---------------|-----------------|---------------------|
| **Wayback Machine** | Historical website snapshots -- pricing changes, messaging pivots, removed pages | `web.archive.org/web/{date}/{url}` | All -- especially SaaS (pricing), E-Commerce (product lines) | API available (free), Clay integration |
| **Google Reviews** | Customer sentiment, operational complaints, location-specific issues | Search `"{company}" reviews site:google.com` or Google Maps API | Food Service, Healthcare, Real Estate, Professional Services | Google Places API, Clay enrichment |
| **OSHA Database** | Workplace safety citations, inspection history, penalties | `osha.gov/ords/imis/establishment.html` | Manufacturing, Logistics, Construction | Direct URL scraping, bulk downloads available |
| **SEC EDGAR** | Public company filings -- 10-K, 10-Q, 8-K, comment letters, insider transactions | `sec.gov/cgi-bin/browse-edgar` | Financial Services, SaaS (public), any public company | EDGAR API (free), full-text search |
| **FMCSA SAFER** | Motor carrier safety records, fleet size, insurance, inspection scores | `safer.fmcsa.dot.gov` | Logistics, Supply Chain, any company with fleet | Bulk data downloads, API |
| **State Licensing DBs** | Professional licenses -- real estate, insurance, food service, healthcare | Varies by state. Search `"{state}" {license type} license lookup` | All regulated industries | Varies -- some have APIs, most are scrapable |
| **Health Dept Records** | Restaurant inspection scores, violations, compliance history | County/city health department websites | Food Service, Hospitality | Varies by jurisdiction |
| **USPTO** | Patent filings, trademark applications -- reveals R&D direction | `patft.uspto.gov` (patents), `tmsearch.uspto.gov` (trademarks) | SaaS, Manufacturing, HealthTech, any IP-driven company | USPTO API (free) |
| **Google Maps** | Location data, hours, photos, Q&A, popular times | Google Maps API or manual search | Multi-location businesses -- Food Service, Retail, Real Estate | Google Places API |
| **County Planning Records** | Building permits, zoning changes, new construction filings | County assessor/planning department websites | Real Estate, Manufacturing, Food Service (new locations) | Usually manual, some counties have APIs |
| **Government Procurement** | RFPs, contract awards, spending data | `sam.gov`, `usaspending.gov`, state procurement portals | Professional Services, SaaS (gov), Education | SAM.gov API, bulk downloads |
| **Census / BLS Data** | Demographics, economic indicators, industry statistics | `census.gov`, `bls.gov` | All -- for market sizing and trend validation | APIs available (free) |
| **Import/Export Records** | Customs data, shipping records, supplier information | `importgenius.com` (limited free), `panjiva.com` | Manufacturing, E-Commerce, Logistics | Paid plans for bulk access |
| **Court Records** | Lawsuits, liens, judgments, bankruptcy filings | PACER (federal), state court websites | All -- especially for risk signals | PACER API, some state APIs |

## Tier 2: Free, Light Auth

Requires free account creation. Worth the setup.

| Source | What It Contains | How to Access | Cost | Best Industries | Automation Potential |
|--------|-----------------|---------------|------|-----------------|---------------------|
| **LinkedIn** | Professional profiles, job postings, company pages, content activity | LinkedIn + search for public data, Sales Nav for deep search | Free (limited), Sales Nav ($99/mo) | All | Apollo/Clay enrichment, search for public |
| **G2** | Software reviews, comparison data, buyer intent signals | `g2.com` -- free to browse, account for full reviews | Free to browse | SaaS, any company buying software | G2 Buyer Intent (paid), search scraping |
| **Capterra** | Software reviews, feature comparisons | `capterra.com` | Free | SaaS, any software buyer | Search scraping |
| **Trustpilot** | Consumer/business reviews, response patterns | `trustpilot.com` | Free | E-Commerce, DTC, Financial Services | Trustpilot API (limited) |
| **Glassdoor** | Employee reviews, salary data, interview insights | `glassdoor.com` | Free (limited) | All -- reveals internal culture and operational issues | Search scraping for public data |
| **GitHub** | Code repositories, commit activity, contributor patterns, open issues | `github.com` | Free | SaaS, DevTools, any company with open source | GitHub API (free, generous limits) |
| **Product Hunt** | Product launches, upvotes, comments, maker engagement | `producthunt.com` | Free | SaaS, DTC, Consumer Tech | Product Hunt API |
| **Indeed/Glassdoor Jobs** | Job postings, salary ranges, role descriptions | `indeed.com`, `glassdoor.com` | Free | All -- job postings reveal strategy | Search scraping, some APIs |
| **Crunchbase (Basic)** | Funding rounds, investors, basic company data | `crunchbase.com` | Free (very limited) | SaaS, FinTech, any VC-backed company | Crunchbase API (paid for bulk) |

## Tier 3: Paid, Structured

Clean data, API access, integrates with enrichment workflows.

| Source | What It Contains | How to Access | Cost | Best Industries | Automation Potential |
|--------|-----------------|---------------|------|-----------------|---------------------|
| **BuiltWith** | Technology stack detection -- CRM, marketing tools, analytics, hosting | `builtwith.com`, API | $295-$495/mo | SaaS, any company with web presence | Clay integration, API, bulk lookups |
| **Apollo** | Contact data, company data, intent signals, sequences | `apollo.io` | $49-$119/mo per user | All | Native API, Clay integration |
| **Crunchbase Pro** | Full funding data, acquisitions, leadership changes, news | `crunchbase.com/pro` | $49/mo (annual) | SaaS, FinTech, VC-backed companies | API, CSV exports, Clay integration |
| **SimilarWeb** | Website traffic, traffic sources, engagement metrics, competitor analysis | `similarweb.com` | $125/mo+ | E-Commerce, SaaS, Media, any digital business | API, Clay integration |
| **SEMrush** | SEO data, paid search, content analysis, keyword rankings | `semrush.com` | $130/mo+ | All -- especially content-heavy businesses | API, bulk analysis |
| **Ocean.io** | Lookalike company discovery, TAM analysis | `ocean.io` | Custom pricing | All -- for finding companies similar to your best customers | API, Clay integration |
| **Clay** | Data enrichment orchestration -- chains multiple sources | `clay.com` | $149-$800/mo | All | Native -- Clay IS the automation layer |
| **ZoomInfo** | Contact + company data, intent, org charts | `zoominfo.com` | $15K+/year | Enterprise sales, all industries | API, CRM integrations |
| **Bombora** | B2B intent data -- who's researching what topics | `bombora.com` | Custom pricing | SaaS, Professional Services | API, CRM integrations |

## Tier 4: Specialized / Niche

Deep domain-specific data. High value for specific angles.

| Source | What It Contains | How to Access | Cost | Best Industries | Automation Potential |
|--------|-----------------|---------------|------|-----------------|---------------------|
| **NMLS** | Mortgage + money transmitter license data, state-by-state | `nmlsconsumeraccess.org` | Free | Financial Services, FinTech | Manual lookup, limited bulk |
| **CMS.gov** | Medicare/Medicaid reimbursement rates, provider data, quality scores | `cms.gov`, `data.cms.gov` | Free | Healthcare, HealthTech | APIs available, bulk downloads |
| **FDA** | Drug approvals, device clearances, warning letters, recalls | `fda.gov`, `openFDA` API | Free | HealthTech, Pharma, Medical Devices | openFDA API (free) |
| **FCC** | Telecom licenses, spectrum auctions, equipment authorizations | `fcc.gov`, ULS database | Free | Telecom, IoT, any wireless product | FCC API |
| **SBA** | Small business loan data, disaster loans, 8(a) certifications | `sba.gov`, `data.sba.gov` | Free | SMB-focused companies, Professional Services | Bulk downloads |
| **NCES** | Education institution data -- enrollment, finances, programs | `nces.ed.gov` | Free | Education, EdTech | IPEDS API, bulk downloads |
| **Grants.gov** | Federal grant opportunities, awards, deadlines | `grants.gov` | Free | Education, Healthcare, Nonprofits | API, RSS feeds |
| **KLAS Research** | Healthcare IT vendor ratings, user sentiment | `klasresearch.com` | Paid (expensive) | HealthTech | Manual access |
| **CoStar** | Commercial real estate data -- rents, vacancies, transactions | `costar.com` | Paid ($300+/mo) | Real Estate, PropTech | API for enterprise |
| **ImportGenius** | Detailed customs/import records, supplier relationships | `importgenius.com` | $99/mo+ | Manufacturing, E-Commerce, Logistics | Search + CSV export |
| **Dun & Bradstreet** | Business credit scores, firmographics, risk data | `dnb.com` | Custom pricing | All B2B -- especially for risk/credit angles | API, bulk enrichment |
| **PitchBook** | VC/PE deal data, valuations, fund performance | `pitchbook.com` | $20K+/year | FinTech, SaaS, VC-backed companies | API for enterprise |

---

## Data Collection Methodology Template

For each data source used in an angle, document:

```markdown
### Data Source: {Name}

**Purpose in this angle:** {Why you need this data}
**Access method:** {URL / API / Tool}
**Query/filter:** {Exact search or API call}
**Expected output:** {What you'll get back}
**Enrichment chain:** {How this feeds into the next step}
**Freshness requirement:** {How often data needs to be refreshed}
**Cost per lookup:** {Approximate cost}

**Integration:**
- [ ] Direct integration available
- [ ] API integration possible
- [ ] Manual lookup required
- [ ] Search scraping viable

**Sample workflow:**
1. {Step 1}
2. {Step 2}
3. {Step 3}
```

---

## Source Selection Heuristic

When choosing data sources for an angle:

1. **Start with Tier 1** -- free, fast, no dependencies. If you can build the angle on Tier 1 alone, do it.
2. **Layer Tier 2** for customer voice -- reviews, employee sentiment, community chatter add the "why" behind the signal.
3. **Use Tier 3** for execution -- once the angle is validated, structured data makes list-building scalable.
4. **Reserve Tier 4** for differentiation -- niche data is what makes an angle truly non-obvious. If competitors don't know the data source exists, the angle's shelf life extends dramatically.

**Rule of thumb:** The best angles combine 1 broad source (Tier 1-2) with 1 niche source (Tier 3-4). The broad source identifies the prospect. The niche source reveals the angle.
