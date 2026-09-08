# Companion note · the `docs/` folder pattern

> Explains **[`docs-template/README.md`](../docs-template/README.md)** — the index file
> for the doc set. Copy the whole `docs-template/` folder into your project as `docs/`;
> see the [folder README](../README.md) for the 5-step setup.

This note is background, not a file you copy.

## Why a `docs/` folder in the repo

Keep the project's durable context as Markdown **in the repo**, next to the code — not in
a wiki, not in Notion, not in a chat tool's private memory. Three reasons:

- **It survives tool changes.** Switch from Cursor to Claude Code to something else next
  year and the context is still there.
- **It versions with the code.** Every doc change rides in the commit that made it true,
  so `git blame` on a doc line tells you when and why.
- **The agent reads it for free at session start** — far cheaper than re-explaining the
  architecture every conversation.

An agent that reads these stops doing three expensive things: re-deriving architecture it
could have been told, re-introducing a library that was deliberately removed, and
inventing business facts instead of asking.

## The one distinction people blur

**Living docs vs. snapshots.** `docs/seo.md` is updated forever — it always reflects
current state. `docs/reports/2026-07-audit.md` is frozen the day it's written. A reader
has to be able to tell whether a claim is current or historical. Never edit a report to
"bring it up to date" — that's what the living doc is for.

## The other rule

**Every doc change is in the same commit as the code change it describes.** A doc that
lags the code is worse than no doc: the agent trusts it and is confidently wrong.
