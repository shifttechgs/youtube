# Companion note · the business reference sheet

> Explains **[`docs-template/business.md`](../docs-template/business.md)** — a
> fill-in-the-blanks sheet of business facts. Copy it (with the rest of
> `docs-template/`) into your project as `docs/business.md`.

This note is background, not a file you copy.

## Why this file exists

Ask an agent to write a service page or a `LocalBusiness` schema block without giving it
the facts, and it will produce something **plausible and wrong** — a made-up price range,
a guarantee the business doesn't offer, a service it doesn't sell. It's not lying on
purpose; it's filling a gap the way autocomplete does.

`business.md` is that gap, filled once with real answers so the agent writes copy and
schema *from these facts* instead of inventing them.

## What goes in it

Identity (legal name, registration, address, the one canonical phone format), the
services table (price, what's included, whether it's bookable or quote-only), the service
area, the operating model, and the review situation (real testimonials or placeholder?
is a count shown in visible copy?).

## The single most important line

**"Services the business does NOT offer"** — listed explicitly. This is what stops the
agent building a service page for something imaginary. On one real project six such pages
shipped and all six had to be removed by migration once the owner reviewed them.

## Rules

- **Source every fact** — which config file, which live page, or "owner confirmed on
  {date}". "Base price R1,200 (`config/services.php`)", not "about R1,200".
- **Date the file.** Re-verify before quoting anything externally if it's aged.
- **Facts only, no marketing voice.** The agent writes the copy; this is its source data.
