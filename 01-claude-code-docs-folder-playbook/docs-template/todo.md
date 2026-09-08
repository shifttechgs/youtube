<!--
docs/todo.md — deferred tasks, each with the reason it's deferred.
No placeholders. Keep it to 3–10 items. If an item can't be acted on yet, say what
unblocks it. This is not a backlog groomer — big someday/maybe lists belong elsewhere.
-->

# Deferred tasks

Things consciously **not** being done yet, and why. If it's just "not started", it
doesn't belong here — this file is for work that's blocked or deliberately postponed, so
nobody re-raises it as if it were forgotten.

Each item: **what**, **why it's deferred**, **what unblocks it**.

<!-- EXAMPLES — replace with yours. -->

- **Analytics / tag manager** — deferred until the custom domain is live. Setting it up
  on the temporary host means re-doing it and polluting historical data. *Unblocks when:*
  DNS points to production.
- **`prefers-reduced-motion` support** — not handled anywhere yet. Deferred to a single
  accessibility pass rather than bolted on per-component. *Unblocks when:* the a11y pass
  is scheduled.
- **Second location page set** — held back to avoid thin/duplicate content. *Unblocks
  when:* there's real per-location search-demand evidence.
- **`aggregateRating.reviewCount` in schema** — currently omitted rather than guessed.
  *Unblocks when:* the owner confirms the real current total.
