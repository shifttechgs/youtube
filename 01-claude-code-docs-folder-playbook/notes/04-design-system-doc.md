# Companion note · documenting the design system

> Explains **[`docs-template/design.md`](../docs-template/design.md)** — typography,
> colour tokens, layout and motion conventions. Copy it (with the rest of
> `docs-template/`) into your project as `docs/design.md`.

This note is background, not a file you copy.

## The goal is one word: consistency

You want the agent to build a new section that **looks like it was always there** —
without you reviewing every pixel. That only works if the decisions are written down
somewhere it reads.

## Document decisions, not CSS

The trap is turning this into a second copy of your stylesheet. It will drift from the
real one and then actively mislead. Instead:

- **Link to the real token file** (`resources/css/app.css`, `tailwind.config`, whatever)
  and say "edit there, not scattered hex values".
- Record the **conventions a token file can't express**: the type scale and where
  `clamp()` is used, the alternating light/white/dark section rhythm, the one
  scroll-reveal mechanism used sitewide, which heavy animation lib is scoped to which
  single page.
- List the **reusable patterns** by name (bento stat grid, numbered accordion FAQ,
  breadcrumb + dark hero) so the agent reaches for those instead of inventing a fourth
  variant.

## The "what NOT to introduce" line

No new front-end library for something the stack already does. No per-page design tokens.
Say it explicitly — it's the design-side equivalent of `instructions.md`'s "removed and
not coming back".
