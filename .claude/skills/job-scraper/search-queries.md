# Search Queries for Job Scraper

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; any skill you add with `/add-portal` is included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** - for portals without a CLI, company career pages, or when a CLI fails.

## Search Sites

Primary:
- **linkedin.com/jobs** - LinkedIn job listings (filter: USA / Houston, TX / Remote); also covered by `linkedin-search` CLI
- **indeed.com** - general US job board
- **boards.greenhouse.io**, **jobs.lever.co**, **jobs.ashbyhq.com** - direct ATS career-page searches for target SaaS companies

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for known target companies (see Priority 2 below)

## Query Categories

Queries are grouped by priority. Each query should be combined with location terms (Houston, TX or "remote") where the site supports it.

### Priority 1: Customer Success / Onboarding / Implementation (primary pivot target)

These match Bernard's strongest and most desired career direction: moving from general customer support into a titled Customer Success, Onboarding, or Implementation role.

```
"onboarding manager" OR "onboarding specialist" remote SaaS -intern
"implementation specialist" OR "implementation consultant" remote SaaS
"customer success manager" remote SaaS
site:jobs.lever.co "customer success manager" remote
site:jobs.ashbyhq.com "customer success" remote SMB
```

### Priority 2: SaaS Payroll & HR Tech domain expertise (target companies)

These match Bernard's deep domain expertise in payroll/HR SaaS platforms - searching adjacent/competitor companies to Homebase.

```
"now hiring" OR "we're hiring" "customer success" Gusto OR Rippling OR Justworks OR TriNet
"customer success" OR "onboarding" hiring Deel OR Remote.com OR Toast OR Square remote
"customer success" OR "implementation" hiring ADP OR Paylocity OR Paycom OR Paycor remote
```

### Priority 3: Account Management / SMB (adjacent role Bernard could pivot into)

```
"account manager" remote SaaS "SMB" -sales -"business development"
site:jobs.lever.co "account manager" SMB remote
```

### Priority 4: Technical Support & broader net (wider search)

```
"technical support specialist" remote SaaS -"field" -"onsite"
site:boards.greenhouse.io OR site:jobs.lever.co "customer success" Houston
```

## Location Filter

When evaluating results, verify the job location fits Bernard's flexibility (fully remote, hybrid, or onsite in Houston). Define acceptable areas:
- Fully remote (USA) - ideal
- Houston, TX and surrounding metro area - ideal
- Hybrid roles requiring occasional Houston office presence - acceptable
- Onsite roles outside the Houston metro area - too far, unless relocation assistance is offered (flag for discussion)

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape onboarding" -> Priority 1 queries + custom onboarding-specific queries
- "/scrape Gusto" -> Priority 2 queries filtered to Gusto + a direct Gusto careers page search
