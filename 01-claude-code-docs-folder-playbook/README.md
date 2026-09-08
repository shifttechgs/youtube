# 01 · The `docs/` folder that makes Claude Code build like a senior dev

> **Video:** _Set Up Claude Code Like This: Cheaper Tokens, Actual 10x Results_ · [watch ▶]({{VIDEO_URL}})
> Part of the [shifttechgs/youtube](../README.md) companion-files repo. This folder is
> **standalone** — everything the video refers to is here, nothing depends on other
> folders.

## What this is

The set of **living documentation templates** I keep in a `docs/` folder inside every
client project. Claude Code reads them at the start of a session so it doesn't
re-litigate settled decisions, re-break things that were deliberately removed, or invent
facts about the business.

Everything here is **genericized**. Every real client detail is a `{{PLACEHOLDER}}` you
fill in. Fork it, gut it, make it yours.

## How to use it

1. Copy the files you want into your own project as `docs/`.
2. Find-and-replace the `{{PLACEHOLDERS}}` (each file lists its own at the top).
3. From then on, **update the doc in the same commit as the code change** it describes.
   A doc that lags the code is worse than no doc — the agent trusts it and is wrong.
4. Point the agent at them. One line in `CLAUDE.md` is enough:
   ```
   Before adding a feature, read docs/instructions.md and docs/memory.md.
   Before SEO or content work, read docs/seo.md and docs/business.md.
   Update the relevant doc in the same commit as any change it describes.
   ```

## The files

| File | Real-project equivalent | What it's for |
|---|---|---|
| [`01-docs-folder-pattern.md`](./01-docs-folder-pattern.md) | `docs/README.md` | Why a `docs/` folder; what each doc covers and what it must *not* |
| [`02-conventions-and-gotchas.md`](./02-conventions-and-gotchas.md) | `docs/instructions.md` | Architecture rules, framework traps, "we tried X, don't bring it back" |
| [`03-project-memory-pattern.md`](./03-project-memory-pattern.md) | `docs/memory.md` | A dated decision log + "standing decisions, don't silently reverse" |
| [`04-design-system-doc.md`](./04-design-system-doc.md) | `docs/design.md` | Document tokens/type/motion so the agent stays visually consistent |
| [`05-business-reference-template.md`](./05-business-reference-template.md) | `docs/business.md` | Fill-in-the-blanks sheet of business facts that drive copy & SEO |
| [`06-seo-geo-playbook.md`](./06-seo-geo-playbook.md) | `docs/seo.md` + audit | Scoreboard method, code-vs-owner split, the no-fabrication rule |
| [`07-deployment-and-verification.md`](./07-deployment-and-verification.md) | `docs/deployment.md` | A deploy pipeline **plus** the step everyone skips: proving it landed |
| [`08-offsite-authority-checklist.md`](./08-offsite-authority-checklist.md) | `docs/citations.md` | Directory citations, NAP consistency, partner & press outreach templates |
| [`09-gbp-post-workflow.md`](./09-gbp-post-workflow.md) | `docs/gbp_posts.md` | A queue → posted log for manual Google Business Profile updates |
| [`SECURITY.md`](./SECURITY.md) | *new* | What never to commit, `.env` discipline, safe token patterns, indexing |

## The one rule that makes all of this work

**Never let the agent fabricate.** No invented reviews, no stock photos passed off as
"before/after", no service pages for services the business doesn't sell, no founder bio
that didn't happen. If the real thing doesn't exist yet, the doc says "needs the owner"
and the feature ships empty. Every file here is built around that.

## Licence

[CC BY 4.0](../LICENSE) — use it commercially, change it, no need to ask. A credit link
back to the channel is appreciated but not required.
