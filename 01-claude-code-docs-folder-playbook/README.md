# 01 · The `docs/` folder that makes Claude Code build like a senior dev

> **Video:** _Set Up Claude Code Like This: Cheaper Tokens, Actual 10x Results_ · [watch ▶]({{VIDEO_URL}})
> Part of the [shifttechgs/youtube](../README.md) companion-files repo. This folder is
> **standalone** — everything the video refers to is here, nothing depends on other
> folders.

## Who this is for

You're building or maintaining a small client site with an AI coding agent (Claude Code,
Cursor, etc.), and you want the agent to stop re-deriving your architecture, re-adding
libraries you deleted, and inventing business facts. You'll copy one folder into your
project, spend ~20 minutes filling in blanks, and add one file to your repo root.

No build step, no dependencies. It's Markdown.

## Get started (≈20 min)

1. **Copy the skeleton into your project:**
   ```sh
   cp -r docs-template /path/to/your-project/docs
   ```
   (or copy the `docs-template/` folder in your editor and rename it to `docs/`). The
   files inside are already named the way your project needs them — `README.md`,
   `instructions.md`, `memory.md`, and so on.

2. **Fill in the blanks.** Open [`PLACEHOLDERS.md`](./PLACEHOLDERS.md). Do one
   find-and-replace pass for the ~24 global `{{TOKENS}}` (business name, domain, stack,
   …), then write real content into the per-file blanks it lists (your services table,
   your SEO scores, your deploy pipeline).

3. **Delete the example scaffolding.** Every illustrative block is inside a collapsed
   `<details>` marked *Example* or an `<!-- EXAMPLE -->` comment. Delete those and the
   `<!-- … -->` header at the top of each file. When `grep -rn '{{' docs/` returns
   nothing, you're done.

4. **Wire it to the agent.** Copy [`CLAUDE.md.example`](./CLAUDE.md.example) to your repo
   root as `CLAUDE.md` (or merge its sections into the one you have). It tells the agent
   which doc to read before which kind of work.

5. **Commit `docs/` on its own.** From then on, update the relevant doc *in the same
   commit* as the code change it describes. A doc that lags the code gets trusted and is
   wrong.

## What's in this folder

| Path | This is… | You…|
|---|---|---|
| **[`docs-template/`](./docs-template/)** | the thing you copy — the actual doc set, one file per `docs/` doc | copy it into your project as `docs/` |
| **[`PLACEHOLDERS.md`](./PLACEHOLDERS.md)** | every `{{TOKEN}}` in one table + the write-by-hand blanks | work through it once, right after copying |
| **[`CLAUDE.md.example`](./CLAUDE.md.example)** | the agent's root instruction file | copy to your repo root as `CLAUDE.md` |
| [`notes/`](./notes/) | optional background — *why* each doc earns its place, one short note per doc, numbered to the video | read for context; nothing here gets copied |
| [`SECURITY.md`](./SECURITY.md) | this repo's security policy | read only if reporting a problem with these templates |

`docs-template/` is the source of truth. If a note in `notes/` and a template ever
disagree, the template wins.

## The one rule that makes all of this work

**Never let the agent fabricate.** No invented reviews, no stock photos passed off as
"before/after", no service pages for services the business doesn't sell, no founder bio
that didn't happen. If the real thing doesn't exist yet, the doc says "needs the owner"
and the feature ships empty. Every file here is built around that.

## Licence

[CC BY 4.0](../LICENSE) — use it commercially, change it, no need to ask. A credit link
back to the channel is appreciated but not required.
