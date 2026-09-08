<!--
TEMPLATE — genericized from a real client project's docs/seo.md + a dated audit report.
Placeholders: {{DOMAIN}} {{DATE}}
The scores below are illustrative. The method is the point, not the numbers.
-->

# SEO & GEO status — living document

Living summary of where SEO / Local SEO / GEO (Generative Engine Optimisation — showing
up in AI answers, not just blue links) stands. The full point-in-time **audit** lives in
`reports/` and is never edited after the day it's written. **This** file tracks current
state and is updated as work progresses.

## Scoreboard (as of {{DATE}})

| Category | Score | Change |
|---|---|---|
| Technical SEO | 78 / 100 | ↑37 |
| Local SEO | 58 / 100 | ↑6 |
| GEO / AI visibility | 45 / 100 | ↑23 |
| E-E-A-T | 60 / 100 | ↑20 |
| Content & topical authority | 54 / 100 | ↑8 |
| Conversion (CRO) | 72 / 100 | ↑4 |
| Backlinks / off-site authority | 15 / 100 | unchanged |
| **Composite** | **59 / 100** | ↑19 |

Read it as: **everything fixable from inside the codebase has moved.** Off-site
authority is flat because nothing in that category can be fixed by editing code — it
needs account-verification and outreach actions only the business owner can do. That
split is the single most useful thing this file communicates.

## The code-vs-owner split

Every open item is tagged with who can actually do it:

**Fixable in code (the agent can do these):**
- Dynamic `robots.txt` that self-corrects from `APP_URL` (never hardcode the domain)
- `LocalBusiness` / service schema sitewide; `FAQPage` on homepage + every service &
  area page; `BreadcrumbList` on every interior page
- Open Graph + Twitter Card meta sitewide
- `noindex` on `/admin/*`, token-gated pages, and any orphaned page — and remove them
  from the sitemap
- Real Privacy Policy + Terms pages (privacy-law-aware for your jurisdiction)
- Sitemap with `<lastmod>` **and** `<priority>` on every URL
- `Organization` + `WebSite` schema on the homepage; enrich `LocalBusiness` with `@id`,
  `legalName`, `logo`, `geo`, `sameAs`
- A dynamic `/llms.txt` generated from the real service/area data (so it can't drift)
- Blog pagination: page 1 indexable, page 2+ `noindex,follow` to avoid thin-page bloat

**Needs the business owner (the agent cannot and must not fake these):**
- Google Business Profile: categories, service area, real photos
- Re-entering any setting that was only fixed in the dev database, on production
- Confirming `aggregateRating.reviewCount` against the **real** current review total
- Submitting the sitemap in Search Console
- Claiming directory listings — see
  [`08-offsite-authority-checklist.md`](./08-offsite-authority-checklist.md)
- Sending the partner / press outreach in that same file
- Supplying real before/after job photos and real additional reviews

## The no-fabrication rule (non-negotiable)

This is where most "SEO automation" quietly goes wrong. The agent does **not**:

- invent reviews or a review count
- use a stock photo as a "before/after" pair — the gallery component **renders nothing**
  until real job photos exist, on purpose
- build a service page for a service the business doesn't actually offer (a real project
  shipped 6 such pages, then had to remove all 6 by migration when the owner reviewed
  them — don't re-add without explicit confirmation)
- write a founder/team bio with any detail that wasn't already public and true
- soften a legal question into a promise — "will I get my deposit back?" gets a
  reframe around the condition checklist, flagged as not legal advice, not a "yes"

If the real asset doesn't exist, the feature ships **empty** and the item moves to the
"needs the business owner" list above.

## Schema conventions

- Build the array in code and `json_encode()` the whole block — never hand-escape JSON-LD
  strings inside templates.
- One `FAQPage` block per page can cover many Q&As; don't emit one per question.
- Keep visible FAQ Q&A **visible** (not hidden behind an accordion `display:none`) —
  more citable for AI Overviews.

## Testing what's automatable

Don't hand-wave "SEO looks fine". A real project asserts, across **every** public page:
self-referencing canonical, unique non-empty `<title>`, non-empty meta description,
`index,follow` robots, descriptive `alt` on every image, and well-formed JSON-LD with
`@type`/`@context` on every block. Plus sitemap coverage: every URL present, every URL
has `<lastmod>` and `<priority>`. That's a test file, not a checklist.

What still needs a live URL: Google's Rich Results Test and Lighthouse / PageSpeed —
run those against the homepage + top 3 pages once the domain is live.

## Constraints to respect

- Don't promise same-day / emergency service in copy if capacity can't back it.
- A bounded set of location pages, not a full service×location matrix — revisit only
  with real per-location search-demand evidence.
- Don't add analytics before the custom domain is live.
