<!--
docs/memory.md — build history + standing decisions.
Placeholders: {{PROJECT}} — see ../PLACEHOLDERS.md
Start your timeline from your first commit. The Example block below shows the shape;
delete it once you have real entries.
-->

# Project memory — {{PROJECT}}

A condensed build history and decision log, kept **in the repo** so the context survives
independent of any one tool's private memory. Two sections: a dated **timeline**, and a
short list of **standing decisions** that must not be silently reversed.

If an entry here conflicts with the current code, the code wins — but that's a signal the
doc is stale; verify and update it.

## Timeline

Newest at the bottom. Each entry: **`YYYY-MM-DD` — one-line headline.** Then 2–5 sentences
on *what changed and why*, not the diff. Name the files touched so a reader can jump
straight to them.

<!-- Your first entry goes here. -->

<details>
<summary><strong>Example — delete once you have real entries</strong></summary>

**2026-01-10 — Landing page built.** Single-page marketing site. Hero includes a location
autocomplete that submits straight to the primary CTA channel.

**2026-02-02 — Blog added, no database.** Metadata in config, bodies as one template per
slug. Added dynamic `sitemap.xml`, `robots.txt`, canonical tags, per-page meta
description.

**2026-03-01 — SEO service & location pages added.** Chosen over building an admin panel
first, because the site had zero indexable pages beyond the homepage. Config-driven (see
[`instructions.md`](./instructions.md)); deliberately *not* a full service×suburb matrix.

**2026-04-06 — SEO/GEO audit + same-day implementation.** Full audit against the live
codebase (see [`reports/`](./reports/)). Confirmed by direct question to the owner: only N
services are real, the domain is bought but DNS not pointed, the GBP is already claimed
with real reviews. Implemented same day: dynamic `robots.txt`, sitewide schema, Open
Graph tags, `noindex` on admin/token pages, real Privacy/Terms pages.

</details>

## Standing decisions (don't silently reverse these)

<!-- EXAMPLES — replace with yours. Each line: the decision, then the reason it exists. -->

- **No database for content** — blog/services/areas stay as static config unless content
  genuinely outgrows it.
- **No payment gateway** — the primary CTA channel is the deliberate flow. Don't
  introduce Stripe/PayPal without being asked.
- **No external permissions package, no admin-panel framework** — explicitly rejected as
  scope creep for a 1–2 person business.
- **A bounded set of location pages, not a full matrix** — deliberate anti-thin-content
  decision. Revisit only with real per-location search-demand evidence.
- **Analytics deferred** until the custom domain is live.
- **Admin invite/reset passwords are only ever shown in the terminal at generation
  time** — never written to a file. If one is lost, reseed or reset.

## How to write a good entry

- Lead with the **decision**, then the **reason**. "Switched X to Y because Z."
- Record what was **rejected** and why — that's what stops the next person redoing it.
- If a change only touched the dev database (a setting, a seeded value), **say so** and
  note that production needs the same change made by hand.
- Convert relative dates to absolute. "Last week" is meaningless in six months.
