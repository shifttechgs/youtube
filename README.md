# shifttechgs · YouTube companion files

Downloadable files for the videos on the channel — templates, playbooks, configs and
prompts you can actually use, not just look at.

## How this repo is organised

**One folder per video. Each folder is completely standalone** — it has its own
`README.md`, all its own files, and never depends on another folder. Grab the one folder
for the video you're watching and ignore the rest.

Folders are numbered in release order:

| # | Folder | Video | What's inside |
|---|---|---|---|
| 01 | [`01-claude-code-docs-folder-playbook/`](./01-claude-code-docs-folder-playbook/) | _Set Up Claude Code Like This: Cheaper Tokens, Actual 10x Results_ | The `docs/` folder templates that give Claude Code durable project context — conventions, memory log, design system, SEO/GEO playbook, deployment, security |

_(new rows added per video)_

## Conventions

- Every file is **genericized**. Real client details are `{{PLACEHOLDERS}}` you replace.
- **No secrets, ever** — see any folder's `SECURITY.md`. If you find something that
  looks like a real credential, open an issue.
- Each folder's `README.md` links the video and explains how to use that folder's files.

## Licence

[CC BY 4.0](./LICENSE) — use commercially, modify, redistribute. Attribution to the
channel is appreciated, not required.

## Adding a folder for a new video (maintainer note)

1. `NN-short-slug/` — next number, kebab-case slug.
2. Inside it: a `README.md` (copy an existing one, keep the header block with
   `{{VIDEO_URL}}`), the files, and a `SECURITY.md` if the video touches deployment,
   secrets, or client data.
3. Add a row to the table above.
4. Keep it self-contained — no `../` references into other video folders.
