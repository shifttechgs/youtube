<!--
TEMPLATE — genericized from a real Laravel/Blade/Tailwind client project.
Placeholders: {{STACK}} {{CONTENT_CONFIG_PATH}} {{PRIMARY_CTA_CHANNEL}}
Keep the *shape* of this file for your own stack; the specific gotchas below are
Laravel/Blade/Alpine examples — replace with yours, but keep the "we tried X, don't
bring it back" entries, that's the highest-value part.
-->

# Working on this project — conventions & gotchas

Practical conventions for anyone (human or AI) picking up this codebase. **Read this
before adding a feature.** Most patterns here exist because an earlier approach was
tried and deliberately replaced — the file is as much "don't do this again" as it is
"do this".

## Stack

{{STACK}} — e.g. Laravel 12, Blade templates, Tailwind CSS v4 (real Vite build, **not**
the CDN), Alpine.js (deferred), one animation library scoped to a single page. MySQL in
dev and production.

## The "static config, not a database" pattern

Content that rarely changes — blog posts, service descriptions, location/area pages —
lives in **config files and templates**, not database models. This is deliberate: it
keeps the site fast to extend without migrations.

- **Services:** one entry in `{{CONTENT_CONFIG_PATH}}` per service (pricing/booking
  logic) + one in a marketing-copy config (headline, FAQs). Adding a service is two
  config entries, no route, no controller, no migration.
- **Areas / locations:** one config array. Keep name casing identical everywhere — if a
  form validates a location by exact string match, a casing drift is a silent bug.
- **Blog:** metadata in config, body content as a template file per slug.

The **only** real database tables are the ones that genuinely need persisted state —
here: `bookings`, `clients`, `users`, `settings`. Capacity checks, CRM history, auth,
and business settings need a database. A list of three services does not. **Don't add a
table for content a config file handles well.**

## One CTA channel, on purpose

Every client-facing call-to-action ends in the same place — here, a
`{{PRIMARY_CTA_CHANNEL}}` link (e.g. a pre-filled WhatsApp message), **not** a payment
gateway and not an email-only form. Reuse that one pattern for every new CTA. Don't
introduce a second channel (Stripe, a contact form, a chatbot) unless explicitly asked —
a small business with one person answering enquiries wants one inbox, not four.

Transactional emails (quote / invoice / confirmation) can exist *alongside* the primary
channel, sent from the admin panel — never silently *instead* of it.

## Framework gotchas (Blade / Alpine examples — swap for your stack's)

- **Inline JSON-LD in Blade:** a bare `@context` / `@type` at the start of a line
  collides with Blade's directive parser. Build the array in a `@php` block and
  `json_encode()` the whole thing — it sidesteps the problem. Use this for *all* new
  schema; don't hand-escape strings.
- **Alpine `x-data` on a double-quoted attribute:** never put a literal `"` inside inline
  JS in a double-quoted `x-data="..."` — it silently truncates the attribute. Use
  unquoted attribute selectors (`meta[name=csrf-token]`) or single-quote the outer.
- **`x-for` `:key`:** must be unique across the array. Keying by a value that can repeat
  (weekday initials `M T W T F S S`) silently collapses duplicates. Key by index.

## Build process

If your CSS is a real compiled build (not a CDN), **run the build before testing any CSS
change** — there's no CDN fallback to mask a stale build. If two stylesheets exist
(e.g. public site vs. admin panel with different button sizing), know which entry point
you're editing.

**Removed and not coming back:** list every library you deliberately deleted and why, so
nobody "helpfully" re-adds it:

- *jQuery* — redundant with the IntersectionObserver fallback already in the code.
- *Carousel library* — its target element no longer exists since testimonials moved to a
  CSS-only scroll animation. If a future feature needs a carousel, build it with the
  framework you already have, not a jQuery-era plugin.
- *Heavy animation libs* — loaded on **one** page only (the homepage hero), via a
  page-scoped script push. Don't move them into the shared layout "for convenience".

## Admin panel

`/admin/*` is gated by auth middleware; a sub-group gates user/role management via a
simple `role` column check — **no external permissions package**. That was explicitly
rejected as scope creep for a 1–2 person business. The hand-built panel is the standing
choice; don't propose Filament / Nova / a permissions package without being asked.
