<!--
docs/instructions.md — codebase conventions & gotchas.
Placeholders: {{STACK}} {{CONTENT_CONFIG_PATH}} {{PRIMARY_CTA_CHANNEL}} — see ../PLACEHOLDERS.md
The framework-specific gotchas below are Laravel/Blade/Alpine EXAMPLES. Replace them with
yours — but keep the "we tried X, don't bring it back" section. That's the highest-value
part of this file.
-->

# Working on this project — conventions & gotchas

Practical conventions for anyone (human or AI) picking up this codebase. **Read this
before adding a feature.** Most patterns here exist because an earlier approach was tried
and deliberately replaced — this file is as much "don't do this again" as it is "do
this".

## Stack

{{STACK}}

Note the things that bite: is the CSS a real build or a CDN? Is there more than one
build entry point (public site vs. admin)? Which database in dev vs. production?

## The "static config, not a database" pattern

<!-- Keep this section only if it's true for your project. Delete otherwise. -->

Content that rarely changes — blog posts, service descriptions, location/area pages —
lives in **config files and templates**, not database models. This is deliberate: it
keeps the site fast to extend without migrations.

- **Services:** one entry in `{{CONTENT_CONFIG_PATH}}` per service (pricing/booking
  logic) + one in a marketing-copy config (headline, FAQs). Adding a service is two
  config entries — no route, no controller, no migration.
- **Areas / locations:** one config array. Keep name casing identical everywhere — if a
  form validates a location by exact string match, a casing drift is a silent bug.
- **Blog:** metadata in config, body content as a template file per slug.

The **only** real database tables are the ones that genuinely need persisted state.
**Don't add a table for content a config file handles well.**

## One CTA channel, on purpose

Every client-facing call-to-action ends in the same place — a `{{PRIMARY_CTA_CHANNEL}}` —
**not** a payment gateway and not an email-only form. Reuse that one pattern for every
new CTA. Don't introduce a second channel (Stripe, a contact form, a chatbot) unless
explicitly asked — a small business with one person answering enquiries wants one inbox,
not four.

Transactional emails (quote / invoice / confirmation) can exist *alongside* the primary
channel — never silently *instead* of it.

## Framework gotchas

<!-- EXAMPLES from a Blade/Alpine project. Delete these, add your own stack's traps. -->

- **Inline JSON-LD in Blade:** a bare `@context` / `@type` at the start of a line
  collides with Blade's directive parser. Build the array in a `@php` block and
  `json_encode()` the whole thing. Use this for *all* new schema; don't hand-escape.
- **Alpine `x-data` on a double-quoted attribute:** never put a literal `"` inside inline
  JS in a double-quoted `x-data="..."` — it silently truncates the attribute.
- **`x-for` `:key`:** must be unique across the array. Keying by a value that can repeat
  (weekday initials `M T W T F S S`) silently collapses duplicates. Key by index.

## Build process

<!-- Keep if your CSS/JS is a real compiled build. -->

Run the build before testing any CSS change — there's no CDN fallback to mask a stale
build. If two stylesheets exist (public site vs. admin panel), know which entry point
you're editing.

## Removed and not coming back

List every library or pattern you deliberately deleted and why, so nobody "helpfully"
re-adds it after seeing an old snippet online.

<!-- EXAMPLES — replace with your project's actual removals. -->

- **jQuery** — redundant with the IntersectionObserver fallback already in the code.
- **Carousel library** — its target element no longer exists since testimonials moved to
  a CSS-only scroll animation. If a future feature needs a carousel, build it with the
  framework you already have.
- **Heavy animation libs** — loaded on **one** page only (the homepage hero), via a
  page-scoped script include. Don't move them into the shared layout "for convenience".

## Admin panel

<!-- Keep if you have one. -->

`/admin/*` is gated by auth middleware; a sub-group gates user/role management via a
simple `role` column check — **no external permissions package**. That was explicitly
rejected as scope creep for a 1–2 person business. Don't propose a permissions package or
an admin-panel framework without being asked.
