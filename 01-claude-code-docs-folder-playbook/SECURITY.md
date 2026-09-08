<!--
TEMPLATE — a security baseline for a small-business site built with an AI coding agent.
Not genericized *from* a client file — written fresh for this playbook.
Placeholders: {{DOMAIN}} {{PRIVACY_LAW}} (e.g. POPIA, GDPR, CCPA)
-->

# Security baseline

The rules that keep a client site — and the repo it lives in — from leaking something
that can't be un-leaked. Written for a solo dev or tiny team working with an AI coding
agent. None of this is optional.

## 1. What never goes in the repo

Not in code, not in a doc, not in a commit message, not in a comment — **not even
briefly**. Git history is forever; a secret pushed once is compromised even if the next
commit removes it.

- `.env` and any real environment file. Commit `.env.example` with **empty** values only.
- API keys, tokens, passwords, private keys, connection strings, webhook URLs with
  embedded secrets.
- The **deploy token**, FTP/SSH credentials, database passwords, mail credentials.
- Real customer data — names, addresses, phone numbers, emails, booking records,
  invoices. Test with synthetic data.
- In a **public** teaching repo like this one: the client's real business identity too —
  legal name, registration number, physical address, direct phone, staff names, review
  URLs. Genericize to `{{PLACEHOLDERS}}`. (Public-facing facts about an already-live site
  can be a named case study *if the client agrees* — secrets still never.)

A `.gitignore` is a safety net, not the rule. The rule is "don't type it into a file
under version control".

## 2. `.env` discipline

- The server's `.env` is created **manually, once**, on the server. CI **never** uploads
  it — CI overwriting the server's own secrets is a real outage waiting to happen.
- Generate the app key on the server (or locally, once) with the framework's key
  command — never reuse a key from another environment, never commit it.
- `APP_DEBUG=false` and `APP_ENV=production` on production, always. A debug stack trace
  on a live site leaks paths, config, and sometimes credentials.
- Rotate any credential the moment you suspect it was exposed. Rotation, not deletion —
  the old value is already in someone's clone or a CI log.

## 3. Token-guarded endpoints (the safe pattern)

Some endpoints must be callable by CI, which can't hold a session or a CSRF token. The
safe shape:

- The endpoint is CSRF-exempt **by design** — document *why*, so nobody "fixes" it.
- Its protection is a **long random token** (32+ bytes) compared in **constant time**
  (`hash_equals` / equivalent) — never `==`, which is timing-attackable.
- Without a valid token it returns **403 and does nothing** — safe to leave deployed
  even when unused.
- The token lives in the server `.env` **and** the CI secret store as the same value.
  It is never logged, never echoed, never in a URL that gets logged.
- Scope it to exactly one job (run migrations + clear caches). It is not a general
  "run a command" endpoint.

## 4. Indexing & access control

- `/admin/*` behind auth middleware. A second check (a `role` column, an `isAdmin()`)
  gates user/role management. Every admin route, no exceptions.
- `noindex` on `/admin/*`, on token-gated pages (`/quote/{token}`, `/invoice/{token}`),
  and on any orphaned page — **and** remove them from `sitemap.xml`. A `noindex` page
  still in the sitemap is a mixed signal.
- Token-gated public pages (client quote/invoice links) use an unguessable token, not a
  sequential ID. Treat the token as the only credential and rate-limit the route.

## 5. Passwords & one-time secrets

- Admin invite / reset passwords are shown **once, in the terminal, at generation
  time** — never written to a file, never emailed in plaintext, never stored in a doc.
  If one is lost, reseed or reset; don't go hunting for it.
- Use the framework's hashing (bcrypt/argon2) for stored passwords. Never a fast hash,
  never home-rolled.

## 6. Privacy law

The site collects personal data (booking forms, lead magnets, contact details). Know
your jurisdiction's law — **{{PRIVACY_LAW}}** — and ship:

- A real Privacy Policy and Terms page that describe what's actually collected and why.
- A lawful basis / consent mechanism for marketing contact.
- A retention answer for booking and lead records — don't keep them forever by default.
- Not "legal advice" language anywhere the site answers a legal-adjacent question;
  reframe around what you actually control.

## 7. Dependencies

- Pin versions. Review what a new package pulls in before adding it.
- Run the ecosystem audit tool (`npm audit`, `composer audit`) in CI; treat a high/critical
  as a build failure.
- Don't reintroduce a removed library because a snippet online used it — check the
  "removed and not coming back" list in
  [`02-conventions-and-gotchas.md`](./02-conventions-and-gotchas.md).

## 8. If a secret lands in git history

1. **Rotate the secret now.** Assume it's public the moment it was pushed.
2. Purge it from history (`git filter-repo`, or BFG) and force-push — coordinate with
   anyone who has a clone.
3. If the repo is public, also assume it was scraped within minutes. Rotation in step 1
   is the only thing that actually protects you; the history rewrite is cleanup.

## 9. Reporting an issue in this repo

These are documentation templates — no runtime, low blast radius. If you spot something
harmful (a placeholder that looks like a real credential, an unsafe pattern presented as
safe), open an issue or contact the channel. Don't post a working exploit.
