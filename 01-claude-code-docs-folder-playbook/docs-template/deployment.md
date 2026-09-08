<!--
docs/deployment.md — how the deploy works + one-time setup + how to prove it landed.
Placeholders: {{DOMAIN}} {{HOST}} {{APP_ROOT}} {{PHP_VERSION}} — see ../PLACEHOLDERS.md
The pipeline below is a PHP / shared-hosting EXAMPLE. Replace with your own. Keep the
"verifying a deploy actually landed" section whatever your stack — that's the part
everyone skips.
No real hostnames, tokens, or credentials appear here — and none should ever appear in
your copy either. See security.md.
-->

# Deployment & verification

How the deploy pipeline works, the one-time setup it needs, and — the part everyone
skips — **how to prove a deploy actually landed.**

## Why the verification section exists

A previous host's auto-deploy silently stopped working. Production served a stale build
for weeks and nobody noticed, because CI never went red. Every pipeline since then
includes an explicit "did it actually land?" step. **Don't assume a push succeeded just
because you didn't see an error.**

## How it works

<!-- EXAMPLE: CI build + push, no SSH. Replace with your pipeline. -->

1. Push to `main` → CI checks out the code, runs the dependency install and the asset
   build (production dependencies only).
2. The built app is uploaded to the server — only changed files transfer.
3. A final step calls a **token-guarded endpoint** on the live site
   (`POST /deploy/migrate`) that runs database migrations and clears caches. This exists
   *specifically because there's no shell access*. It returns 403 without the token, so
   it's safe to leave in place.

Why an HTTP endpoint and not a session-protected form: CI can't send a session-based CSRF
token. The endpoint is CSRF-exempt **by design**, and its real protection is a
constant-time comparison of a long random `DEPLOY_TOKEN`. Don't "fix" the CSRF exemption
— you'll break CI. Don't log the token. See [`security.md`](./security.md).

## One-time setup (needs host/control-panel access — the agent can't do this)

<!-- EXAMPLE steps for PHP shared hosting. Replace with yours. -->

1. **Point the domain at the framework's public folder**, not the project root. Upload
   the whole app to `{{APP_ROOT}}` and set the document root to `{{APP_ROOT}}/public`.
2. **Runtime version:** set to `{{PHP_VERSION}}` (or your framework's minimum).
3. **Database:** create the production database + user; note the credentials for the
   server's environment file.
4. **Writable directories:** confirm cache/session/log/compiled-view dirs are writable by
   the web user.
5. **Server environment file:** created **manually, once**, never uploaded by CI. Real
   production values: `APP_ENV=production`, `APP_DEBUG=false`,
   `APP_URL=https://{{DOMAIN}}`, a generated app key, the database credentials, and a long
   random `DEPLOY_TOKEN`.
6. **CI secrets:** host, username, password, remote directory, deploy URL, and the
   **same** `DEPLOY_TOKEN` value as the server. Store them in the CI provider's secret
   store — never in the repo.
7. **First deploy is different from every deploy after it:** the app can't boot until the
   environment file + app key exist and the database has been migrated once.

## Verifying a deploy actually landed

After every push, check — don't assume:

```
curl -I https://{{DOMAIN}}/about        # expect 200, not 404
curl -s https://{{DOMAIN}}/ | grep -c "cdn.tailwindcss.com"   # expect 0 (real build, not CDN)
```

Add one or two checks specific to *this* deploy — a string that should now be present, a
route that should now exist. If anything looks wrong, open the CI run and look for a red
❌ **before** assuming it's a hosting-side problem.

## If shell access turns out to be available

Switch the upload step to `rsync`-over-SSH, and the final step to running the migrate +
cache-clear commands directly. Simpler, and it removes the need for the token-guarded
endpoint (no harm leaving it in place, unused).
