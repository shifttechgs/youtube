<!--
docs/design.md — design system, documented for an agent.
Placeholders: {{FONT}} {{TOKEN_FILE}} {{TOKEN_FILE_ADMIN}} — see ../PLACEHOLDERS.md
Hex values below are placeholders — swap for your palette, or delete the table and link
your real token file instead.
-->

# Design system

The point of this file is **consistency**: the agent should be able to build a new
section that looks like it was always there, without you reviewing every pixel. Document
the decisions, link to the real token file, don't duplicate the CSS.

## Typography

- **Font:** {{FONT}}
- Body copy clusters around `13–16px`. Headings scale from `text-3xl` (section headers)
  to `~80px` (homepage hero), using `clamp()` on the few headings that need responsive
  sizing — not breakpoint-specific overrides.
- Tracking: tightened on headings (`tracking-tight`), loosened on small uppercase labels
  (`tracking-[0.18em]` on eyebrow/kicker text).

## Colour tokens

Defined as design-system tokens in **{{TOKEN_FILE}}** (public site) and
**{{TOKEN_FILE_ADMIN}}** (admin, if separate). Edit the token file, not scattered hex
values.

<!-- EXAMPLE palette — replace with yours. -->

| Token | Hex | Use |
|---|---|---|
| `primary` | `#081d3a` | Headings, dark sections, primary button text |
| `primary-deep` | `#040f1f` | Darkest sections, deepest gradients |
| `accent` | `#f6e304` | CTAs, badges, highlight borders, active states |
| `muted` | `#647082` | Secondary/body text on light backgrounds |
| `light` | `#f8f9fc` | Light section backgrounds (alternates with white) |

Composed component classes that aren't simple colour utilities (`.btn-primary`,
`.btn-outline`, `.card`, `.nav-link`) live in the same token file — **check the existing
definition before adding a near-duplicate class.**

## Layout conventions

<!-- EXAMPLES — replace with your project's shared containers/spacing. -->

- `.section-wrap` — the shared max-width (`80rem`) + responsive horizontal padding
  container used by every full-width section. Wrap new section content in this rather
  than hand-rolling padding.
- `.section-py` — shared vertical section padding (`5rem`, `7rem` at `lg:`).
- **Alternating light / white / dark section backgrounds** is the standing rhythm down
  every page. New sections fit the alternation; they don't introduce a new background
  colour.

## Motion

<!-- EXAMPLES — replace with yours. -->

- One scroll-reveal mechanism, sitewide, as the default entrance for new section content
  (IntersectionObserver-driven fade).
- Heavy animation libraries (GSAP-class) are scoped to **one page only** (the homepage
  hero), via a page-scoped script include. Don't add them elsewhere.
- `prefers-reduced-motion` is **not** currently respected anywhere — flag it for the
  accessibility pass, don't assume it's handled.

## Patterns worth reusing

<!-- EXAMPLES — list your project's actual reusable sections. -->

- **Bento stat grid** — asymmetric grid of stat/image/copy tiles on a dark background.
  Good for any "why trust us" section.
- **Accordion FAQ** — single-open-at-a-time, numbered. Reused per-service and per-area.
- **Breadcrumb + dark hero** — every interior page opens with a dark hero containing a
  `/`-separated breadcrumb trail, then the page H1.

## What NOT to introduce

- No new front-end libraries for things the current stack already does (carousels,
  scroll triggers). Use what's there.
- No per-page design tokens. Extend the existing token file rather than hardcoding a
  one-off hex with arbitrary-value syntax.
