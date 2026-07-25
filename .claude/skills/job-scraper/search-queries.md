# Search Queries for Job Scraper

<!-- SETUP: Customize these queries based on your skills, target roles, and location -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

## Search Sites

Primary:
- **indeed.com** - large general US job board
- **linkedin.com/jobs** - LinkedIn job listings (filter: United States / Charlotte, NC, or remote); also covered by `linkedin-search` CLI
- **glassdoor.com** - general US job board, also useful for company/culture research
- **ziprecruiter.com** - general US job board
- **freehire.me** - covered by `freehire-search` CLI

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for known target companies

## Query Categories

Queries are grouped by priority. Each query should be combined with your location terms (e.g. your city, region, or metro area) where the site supports it.

### Priority 1: Manager / PMO Roles

These match your strongest and most desired career direction.

```
site:indeed.com "Manager" "PMO" Charlotte NC
site:indeed.com "Program Manager" SOX Charlotte NC
site:linkedin.com/jobs "PMO Manager" United States
site:linkedin.com/jobs "Program Manager" remote
```

### Priority 2: Data Analyst / SOX-Controls Roles

These match your domain expertise.

```
site:indeed.com "Data Analyst" SQL Python remote
site:indeed.com "Data Analytics Manager" Charlotte NC
site:linkedin.com/jobs "Data Analyst" SOX OR ITGC United States
site:glassdoor.com "Data Analyst" automation remote
```

### Priority 3: Adjacent Roles

Adjacent roles you could pivot into.

```
site:indeed.com "Business Intelligence Analyst" SQL Charlotte NC
site:indeed.com "Risk and Controls" SOX Manager remote
site:linkedin.com/jobs "Technical Program Manager" automation United States
```

### Priority 4: Broader Automation / Consulting

Wider net for general technical/consulting roles.

```
site:indeed.com "automation" PMO Charlotte NC
site:linkedin.com/jobs "SQL" "PMO" remote
site:ziprecruiter.com "Data Analyst" OR "Program Manager" remote
```

## Location Filter

Benjamin is open to relocation and remote work, so this is a soft filter rather than a hard commute check. Define acceptable areas:
- Charlotte, NC and surrounding areas (current home base)
- Remote (anywhere in the US) - preferred
- Any US city, given openness to relocation
- Roles requiring constant/frequent travel are a deal-breaker regardless of location (see Deal-breakers in CLAUDE.md)

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries
