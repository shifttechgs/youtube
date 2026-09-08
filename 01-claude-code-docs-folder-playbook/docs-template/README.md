<!--
============================================================================
SETUP (delete this whole comment once you're done)

You're reading the copy that ships in the playbook. To use it:

  1. Copy this folder into your project:  cp -r docs-template your-project/docs
  2. Work through ../PLACEHOLDERS.md — one find-and-replace pass for the global
     {{TOKENS}}, then write the per-file blanks it lists.
  3. Delete every block marked *Example* (collapsed <details> or <!-- EXAMPLE -->)
     and the <!-- ... --> header at the top of each file.
  4. Copy ../CLAUDE.md.example to your repo root as CLAUDE.md.
  5. Delete any doc you won't maintain, plus its row in the table below.
  6. Commit the whole docs/ folder in its own commit.

Done when `grep -rn '{{' docs/` returns nothing.
This file has no real tokens of its own.
============================================================================
-->

# Project docs

A small folder of Markdown docs kept **in the repo**, next to the code — not in a wiki,
not in Notion, not in a chat tool's private memory. Versioned with the code, so the
context survives independent of any one tool and every doc change rides along with the
commit that made it true.

An AI coding agent that reads these at the start of a session stops doing three expensive
things:

1. Re-deriving architecture it could have been told.
2. Re-introducing a library or pattern that was **deliberately removed**.
3. Inventing business facts (prices, service list, review counts) instead of asking.

## What each file is for

| File | What it covers | What it must **not** become |
|---|---|---|
| `README.md` | This index. One line per doc. | A changelog. |
| `instructions.md` | Codebase conventions and gotchas — read before adding a feature. | A tutorial for the framework; assume the reader knows it. |
| `memory.md` | Build history and standing decisions, newest first. | A diff. Record the *decision and why*, not the code. |
| `design.md` | Colours, typography, layout/motion conventions. | A second copy of the CSS. Link to the real token file. |
| `business.md` | Business facts — services, pricing, area, operating model. | Marketing copy. Facts only, each with a source. |
| `seo.md` | Current SEO/GEO status — living, update as work progresses. | A dated audit. Snapshots go in `reports/`. |
| `deployment.md` | How the deploy pipeline works + one-time setup it needs. | Secrets. Names of secrets are fine; values never. |
| `citations.md` | Off-site authority — directory listings, partnerships, PR. | Tasks the agent can do. This file is owner-action prep. |
| `gbp_posts.md` | Queue + log of manual Google Business Profile posts. | An auto-poster. Every entry ties to something real. |
| `security.md` | What never to commit, `.env` discipline, safe token patterns. | Optional reading. |
| `todo.md` | Deferred tasks with the reason they're deferred. | A backlog groomer. 3–10 items, each unblockable. |
| `reports/` | Dated, point-in-time reports (audits, strategy). | Living documents. These are snapshots; don't edit them later. |

Delete the rows for files you don't keep. Add rows for ones you add.

## Rules

- **Living vs. snapshot.** `seo.md` is updated forever. `reports/2026-07-audit.md` is
  frozen the day it's written. Never blur the two — a reader needs to know whether a
  claim is current or historical.
- **Every doc change is in the same commit as the code change** that made it true. A doc
  that lags the code will be trusted and be wrong.
- **Newest carries the most weight.** In `memory.md`, if the bottom of the file
  contradicts the top, the bottom wins — but say so explicitly and tell the reader to
  verify against the actual files.
- **Facts cite a source.** "Base price R1,200 (`config/services.php`)" not "Base price is
  about R1,200".
- **No secrets, ever.** See [`security.md`](./security.md). Referring to a `DEPLOY_TOKEN`
  env var is fine; pasting its value is a leak that lives in git history forever.

## Wiring it to the agent

The repo root `CLAUDE.md` points the agent here. The core of it:

```
Before adding a feature, read docs/instructions.md and docs/memory.md.
Before SEO or content work, read docs/seo.md and docs/business.md.
Update the relevant doc in the same commit as any change it describes.
```
