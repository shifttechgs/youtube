# Companion note · conventions & gotchas

> Explains **[`docs-template/instructions.md`](../docs-template/instructions.md)** — the
> "read this before adding a feature" doc. Copy it (with the rest of `docs-template/`)
> into your project as `docs/instructions.md`.

This note is background, not a file you copy.

## What this doc is

Practical conventions for anyone — human or AI — picking up the codebase: the stack, the
patterns you've committed to, the framework traps that have bitten you.

## The highest-value section is "Removed and not coming back"

Most conventions in a mature project exist because an **earlier approach was tried and
deliberately replaced**. Without that written down, the next person — or the agent,
prompted by a snippet it found online — helpfully re-adds jQuery, re-introduces the
carousel library whose target element no longer exists, or moves the heavy animation lib
into the shared layout "for convenience".

So the doc isn't just "do this". Half of it is "we did X, it caused Y, don't bring it
back". That section pays for the whole file the first time it stops a regression.

## Write your stack's traps, not the template's

The gotchas in the template file are Laravel/Blade/Alpine examples (Blade eating a bare
`@context` in JSON-LD, Alpine `x-data` truncating on a literal quote, `x-for :key`
collapsing duplicates). Delete them. Yours will be different — but every stack has three
or four, and they're worth the two sentences each.

## Also here: the "static config, not a database" call

If content that rarely changes (services, area pages, blog metadata) lives in config
files rather than database tables, say so and say why — otherwise someone adds a
migration for a list of three services.
