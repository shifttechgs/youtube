# Companion note · the project-memory pattern

> Explains **[`docs-template/memory.md`](../docs-template/memory.md)** — a dated decision
> log plus a list of standing decisions. Copy it (with the rest of `docs-template/`) into
> your project as `docs/memory.md`.

This note is background, not a file you copy.

## Why not just use `git log`

`git log` records *what changed*. It doesn't record *why you chose it* or *what you
rejected on the way*. Six months later, "why isn't this a database table?" has no answer
in the history — the answer was a conversation.

`memory.md` is that conversation, condensed. Two sections:

- **Timeline** — dated entries, newest at the bottom. Each: `YYYY-MM-DD` + a one-line
  headline, then 2–5 sentences on the decision and the reason. Name the files touched.
- **Standing decisions** — the short list of "don't silently reverse these" (no payment
  gateway, no permissions package, bounded location pages, …). The agent treats these as
  binding.

## What makes an entry worth writing

- Lead with the **decision**, then the **reason**: "Switched X to Y because Z."
- Record what was **rejected** and why — that's the part that stops the next person
  redoing the analysis.
- If a change only touched the dev database, **say so**, and note that production needs
  the same change by hand.
- Absolute dates only. "Last week" is meaningless when you read it in a year.

## If it conflicts with the code

The code wins — but that's a signal the doc is stale. Verify and update it in your next
commit.
