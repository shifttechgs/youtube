# Companion note · the SEO / GEO playbook

> Explains **[`docs-template/seo.md`](../docs-template/seo.md)** — a living SEO/GEO status
> doc. Copy it (with the rest of `docs-template/`) into your project as `docs/seo.md`.
> Dated audits go in `docs/reports/`, never in this file.

This note is background, not a file you copy.

## The scoreboard method

Score each category out of 100 (Technical, Local, GEO/AI visibility, E-E-A-T, Content,
CRO, Backlinks) and track the change since last time. The numbers matter less than what
the pattern shows.

## The code-vs-owner split — the useful part

Tag every open item with **who can actually do it**:

- **Fixable in code** — dynamic `robots.txt` from `APP_URL`, sitewide schema, Open Graph
  tags, `noindex` on admin/token pages, real Privacy/Terms pages, a generated `/llms.txt`.
  The agent does these.
- **Needs the business owner** — GBP categories and photos, submitting the sitemap in
  Search Console, confirming the real review count, claiming directory listings, sending
  outreach. The agent **cannot and must not fake these**.

When the code column moves and the off-site column stays flat, that's the doc doing its
job: it's telling you the remaining work is account-verification and outreach, not
editing.

## The no-fabrication rule (non-negotiable)

This is where most "SEO automation" quietly goes wrong. The agent does **not** invent
reviews or a review count, does not pass a stock photo off as a before/after (the gallery
renders nothing until real photos exist — on purpose), does not build a page for a
service the business doesn't offer, does not write a founder bio with any detail that
wasn't already public and true, and does not soften a legal question into a "yes".

If the real asset doesn't exist, the feature ships **empty** and the item moves to the
"needs the owner" list.

## What you can actually test

Assert across every public page: self-referencing canonical, unique non-empty `<title>`,
non-empty meta description, `index,follow`, `alt` on every image, well-formed JSON-LD.
Plus full sitemap coverage. That's a test file, not a vibe check. Rich Results Test and
Lighthouse need a live URL — run them once the domain is up.
