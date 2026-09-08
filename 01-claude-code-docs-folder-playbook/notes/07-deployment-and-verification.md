# Companion note · deployment & verification

> Explains **[`docs-template/deployment.md`](../docs-template/deployment.md)** — how the
> deploy works, the one-time setup it needs, and how to prove it landed. Copy it (with
> the rest of `docs-template/`) into your project as `docs/deployment.md`.

This note is background, not a file you copy.

## The war story that makes this doc exist

On one project, a host's auto-deploy silently stopped working. Production kept serving a
build from *before the admin panel and booking system existed* — for weeks — and nobody
noticed, because CI never went red. A push with no error is not a deploy.

So every deployment doc since then ends with an explicit **"did it actually land?"**
section:

```
curl -I https://example.com/about        # expect 200, not 404
curl -s https://example.com/ | grep -c "cdn.tailwindcss.com"   # expect 0 — real build, not CDN
```

Plus one or two checks specific to *this* deploy — a string that should now be present, a
route that should now exist.

## The token-guarded endpoint pattern

When CI has no shell access, a `POST /deploy/migrate` endpoint runs migrations and clears
caches. It's CSRF-exempt **by design** (CI can't hold a session token) and protected by a
constant-time comparison of a long random `DEPLOY_TOKEN`. Without the token it returns
403 and does nothing, so it's safe to leave deployed. Document *why* it's CSRF-exempt so
nobody "fixes" it and breaks CI.

## The setup the agent can't do

Pointing the domain at `public/`, setting the runtime version, creating the production
database, writing the server's `.env` **by hand once** (CI must never overwrite the
server's own secrets), and putting the same `DEPLOY_TOKEN` in the CI secret store. List
these so it's clear they're owner tasks, not agent tasks.

## Replace the pipeline, keep the verification

The template's pipeline is a PHP / shared-hosting example. Swap in yours. The "prove it
landed" habit transfers to any stack.
