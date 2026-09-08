# Security

## This folder

These are **documentation templates** — Markdown, no runtime, low blast radius. They
contain `{{PLACEHOLDER}}` values, not real credentials or personal data.

If you spot something harmful — a placeholder that looks like a real credential or token,
an unsafe pattern presented as safe, a real business identity that slipped through the
genericization — open an issue or contact the channel. **Don't post a working exploit.**

## The security baseline you copy into your project

The actual security rules — what never goes in the repo, `.env` discipline, the
token-guarded endpoint pattern, indexing and access control, handling a secret that
landed in git history — live in
**[`docs-template/security.md`](./docs-template/security.md)**. That file is copied into
your project as `docs/security.md` along with the rest of `docs-template/`.

Start there. None of it is optional.

## The rule in one line

Never type a real secret into a file under version control — not code, not a doc, not a
commit message, not a comment, not even briefly. Git history is forever; a secret pushed
once is compromised even if the next commit removes it. If it happens, **rotate the
secret first**, then clean up history.
