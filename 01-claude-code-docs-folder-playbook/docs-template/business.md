<!--
docs/business.md — the fill-in-the-blanks sheet of business facts.
Placeholders: {{BUSINESS_NAME}} {{DATE}} {{LEGAL_NAME}} {{REG_NUMBER}} {{ADDRESS}}
{{PHONE}} {{EMAIL}} {{DOMAIN}} and the per-row service/area blanks — see ../PLACEHOLDERS.md
The value of this file is that the agent writes copy and schema from THESE facts instead
of inventing plausible-sounding ones. Source every fact; date the file.
-->

# Business reference — {{BUSINESS_NAME}}

Facts that inform copy, SEO, and product decisions. **Source each fact** from the
codebase (config defaults, config files, live templates) or a direct answer from the
owner. Treat as accurate **as of {{DATE}}**; re-verify before quoting externally if this
file ages.

## Identity

- **Name:** {{BUSINESS_NAME}} — exact casing/spelling as it appears in the logo.
- **Registration / legal name:** {{REG_NUMBER}} / {{LEGAL_NAME}}
- **Address:** {{ADDRESS}} — public walk-in premises, or service-area business? Is the
  address already public (e.g. a map link on the site)?
- **Phone / primary contact channel:** {{PHONE}}
- **Email:** {{EMAIL}} — must be identical across footer, CTAs, legal pages, schema.
  Check the framework's fallback default doesn't point somewhere else.
- **Domain:** {{DOMAIN}} — live? DNS pointed? Any old host URL still resolving?

## Services

For each service record: name, price (fixed / "from" / custom-quote-only), what's
included at the base price, average time, pricing unit, and whether it's bookable through
an automated flow or routed to a manual quote.

| Service | Price | Included at base | Avg time | Unit | Bookable? |
|---|---|---|---|---|---|
| _service name_ | _price_ | _what's included_ | _time_ | _unit_ | yes / quote-only |

- **Add-ons and scaling:** _how extra units / larger jobs are priced_
- **Is published pricing an estimate?** If yes, say so and describe the confirmation step
  (e.g. free on-site inspection, client approval before work).
- **Services the business does NOT offer** — list them explicitly. This is what stops the
  agent building a service page for something imaginary.

## Service area

- **Locations with a dedicated page:** _list_
- **Locations named elsewhere (autocomplete, schema) but with no page yet:** _list_ —
  and the reason (usually: avoid thin/duplicate content until there's real demand).
- **Geographic outliers** worth a capacity gut-check (a location much further from base
  than the rest)?

## Operating model

- **Availability:** _days / hours_
- **Capacity:** _max bookings per day_ — per day total, or per service?
- **Booking flow:** _description_ — ends where? (primary CTA channel / DB record / both)
- **Trust claims already made in public copy:** insured? background-checked staff?
  satisfaction guarantee (what exactly)? free inspection? Only list claims that are
  actually true and already published.

## Reviews

- **Sources:** _Google / other_ — are the on-site testimonials real (traceable to actual
  reviewers) or placeholder?
- **Rating shown:** _rating_. Is a review **count** shown in visible copy? (A hardcoded
  count goes stale fast — many sites remove it from visible text but keep it in schema,
  where it's a data-accuracy question.)
- **Google Business Profile:** claimed? has real reviews?

## Admin / back office

- Panel location, what it manages, the booking status workflow.
- **Payment:** gateway or manual (cash/EFT tracked by hand)?
- **Banking details for invoices** are configured in _where_ and are deliberately **not**
  reproduced in this file.

## Deployment

One line + link to [`deployment.md`](./deployment.md). Note the current host and anything
migrated away from.
