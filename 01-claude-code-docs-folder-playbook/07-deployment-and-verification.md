<!--
TEMPLATE — genericized from a real client project's docs/deployment.md.
Placeholders: {{DOMAIN}} {{HOST}} {{APP_ROOT}} {{PHP_VERSION}}
No real hostnames, tokens, or credentials appear here — and none should ever appear in
your copy either. See SECURITY.md.
-->

# Deployment & verification

How the deploy pipeline works, the one-time setup it needs, and — the part everyone
skips — **how to prove a deploy actually landed.**

## Why the verification section exists

A previous host's auto-deploy silently stopped working. Production served a build from
*before the admin panel and booking system existed* and nobody noticed for weeks,
because CI never went red. Every pipeline since then includes an explicit "did it
actually land?" step. **Don't assume a push succeeded just because you didn't see an
error.**

## How it works (example: CI build + push, no SSH)

1. Push to `main` → CI checks out the code, runs the dependency install and the asset
   build (`--no-dev` for production dependencies).
2. The built app is uploaded to the server — only changed files transfer.
3. A final step calls a **token-guarded endpoint** on the live site
   (`POST /deploy/migrate`) that runs database migrations and clears caches. This exists
   *specifically because there's no shell access* to run those commands directly. If
   shell access appears later, swap this step for a direct command and leave the
   endpoint dormant (it returns 403 without the token, so it's safe to leave in place).

Why an HTTP endpoint and not a session-protected form: CI can't send a session-based
CSRF token. The endpoint is CSRF-exempt **by design**, and its real protection is a
constant-time comparison of a long random `DEPLOY_TOKEN`. Don't "fix" the CSRF exemption
— you'll break CI. Don't log the token. See [`SECURITY.md`](./SECURITY.md).

## One-time setup (needs host/control-panel access — the agent can't do this)

1. **Point the domain at the framework's public folder**, not the project root. Upload
   the whole app to `{{APP_ROOT}}` and set the document root to `{{APP_ROOT}}/public`.
2. **PHP / runtime version:** set to `{{PHP_VERSION}}` (or your framework's minimum).
3. **Database:** create the production database + user; note the name/user/password for
   the server's environment file.
4. **Writable directories:** confirm the cache/session/log/compiled-view directories are
   writable by the web user.
5. **Server environment file:** created **manually, once**, never uploaded by CI (CI
   must never overwrite the server's own secrets). Real production values:
   `APP_ENV=production`, `APP_DEBUG=false`, `APP_URL=https://{{DOMAIN}}`, a generated
   app key, the database credentials, and a long random `DEPLOY_TOKEN`.
6. **CI secrets:** host, username, password, remote directory, deploy URL, and the
   **same** `DEPLOY_TOKEN` value as the server. Store them in the CI provider's secret
   store — never in the repo.
7. **First deploy is different from every deploy after it:** the app can't boot until
   the environment file + app key exist and the database has been migrated once.

## Verifying a deploy actually landed

After every push, check — don't assume:

```
curl -I https://{{DOMAIN}}/about        # expect 200, not 404
curl -s https://{{DOMAIN}}/ | grep -c "cdn.tailwindcss.com"   # expect 0 (real build, not CDN)
```

Add one or two checks that are specific to *this* deploy — a string that should now be
present, a route that should now exist. If anything looks wrong, open the CI run and
look for a red ❌ **before** assuming it's a hosting-side problem.

## If shell access turns out to be available

Switch the upload step to `rsync`-over-SSH, and the final step to running the migrate +
cache-clear commands directly. Simpler, and it removes the need for the token-guarded
endpoint (no harm leaving it in place, unused).
