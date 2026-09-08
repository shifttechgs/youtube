# Placeholders

Every blank in [`docs-template/`](./docs-template/) is one of two kinds.

1. **Global tokens** — `{{LIKE_THIS}}`, listed in the table below. Each means the same
   thing everywhere it appears, so you replace it with **one find-and-replace pass** over
   the whole `docs/` folder before you touch anything else.
2. **Per-file blanks** — either short italic prompts (`_price_`, `_/100_`) in the body of
   a file, or `{{ALL_CAPS}}` tokens inside an email/post template. These aren't swaps —
   you **write real content** in their place. They're listed per file at the bottom.

After both passes, delete the `<!-- comment -->` header at the top of each file and every
block marked *Example* (they're inside collapsed `<details>` or `<!-- EXAMPLE -->`
markers).

---

## Global tokens

Run one find-and-replace per row, across all of `docs/`.

| Token | What it is | Example | Appears in |
|---|---|---|---|
| `{{PROJECT}}` | Short project / repo slug, for the `memory.md` title | `sparkle-web` | memory |
| `{{BUSINESS_NAME}}` | Public trading name, exact casing as on the logo | `Sparkle Home Cleaning` | business, citations |
| `{{LEGAL_NAME}}` | Registered legal entity name | `Sparkle Home Cleaning (Pty) Ltd` | business, citations |
| `{{REG_NUMBER}}` | Company registration number | `2021/123456/07` | business, citations |
| `{{ADDRESS}}` | Full postal address, or a service-area statement if no premises | `12 Main Rd, Claremont, Cape Town 7708` | business, citations |
| `{{PHONE}}` | Primary phone in **one** canonical format used everywhere | `+27 21 555 0123` | business, citations |
| `{{EMAIL}}` | Primary contact email — identical in footer, CTAs, legal pages, schema | `hello@sparkleclean.co.za` | business, citations |
| `{{DOMAIN}}` | Production domain — no scheme, no trailing slash | `sparkleclean.co.za` | business, seo, deployment, citations, gbp_posts, security |
| `{{DATE}}` | Date the fact-set / scoreboard was last verified (ISO 8601) | `2026-09-08` | business, seo |
| `{{HOURS}}` | Operating hours, one line | `Mon–Fri 08:00–17:00, Sat 08:00–13:00` | citations |
| `{{LOGO_URL}}` | Absolute URL to the logo / profile image | `https://sparkleclean.co.za/img/logo-512.png` | citations |
| `{{PRIMARY_CATEGORY}}` | Main GBP / directory category | `House cleaning service` | citations |
| `{{SERVICE_AREA}}` | Geographic area served, as you'd write it in a profile | `Cape Town southern suburbs` | citations |
| `{{AREA}}` | Short area label used inline in copy | `Cape Town` | citations, gbp_posts |
| `{{PRIMARY_CTA_CHANNEL}}` | Where every call-to-action ends up | `a pre-filled WhatsApp message` | instructions |
| `{{STACK}}` | One-line stack summary | `Laravel 12, Blade, Tailwind v4 (Vite build), Alpine.js, MySQL` | instructions |
| `{{CONTENT_CONFIG_PATH}}` | Path to the main services / content config | `config/services.php` | instructions |
| `{{FONT}}` | Primary typeface + how it's loaded | `Inter, via <link>, weights 300–800` | design |
| `{{TOKEN_FILE}}` | Path to the design-token / theme file (public site) | `resources/css/app.css` | design |
| `{{TOKEN_FILE_ADMIN}}` | Design-token file for admin UI, if separate — else delete the mention | `resources/css/admin.css` | design |
| `{{HOST}}` | Hosting provider / environment | `Afrihost shared, cPanel` | deployment |
| `{{APP_ROOT}}` | Deploy path on the server | `/home/sparkle/app` | deployment |
| `{{PHP_VERSION}}` | Runtime version (or your framework's runtime + version) | `8.3` | deployment |
| `{{PRIVACY_LAW}}` | The privacy law governing your users | `POPIA` | security |

### One-liner (macOS / Linux, from inside your project's `docs/`)

```sh
# edit the pairs, then run once
sed -i '' \
  -e 's/{{PROJECT}}/sparkle-web/g' \
  -e 's/{{BUSINESS_NAME}}/Sparkle Home Cleaning/g' \
  -e 's#{{DOMAIN}}#sparkleclean.co.za#g' \
  *.md reports/*.md
# (GNU sed: use `sed -i` without the '' argument)
```

Prefer your editor's project-wide find-and-replace — it's easier to review, and it
handles the tokens with `/` in the value (paths, URLs) without escaping.

---

## Per-file blanks (write, don't swap)

### `business.md`
The whole **Services** table and the italic prompts under each heading (`_price_`,
`_max bookings per day_`, `_description_`, …). Fill from config files or a direct answer
from the owner, and **source each fact**.

### `seo.md`
The `_/100_` cells in the scoreboard, the "Change" column, and the project-specific
bullets under *Fixable in code* and *Constraints to respect*.

### `memory.md`
Your first real timeline entry, and the *Standing decisions* list.

### `design.md`
The colour-token table, layout-container names, motion mechanisms, and reusable patterns
— all currently EXAMPLE values.

### `deployment.md`
The entire *How it works* and *One-time setup* sections are a PHP / shared-hosting
example. Replace with your actual pipeline. Keep *Verifying a deploy actually landed*.

### `citations.md` — email/post templates
`{{PARTNER_RELEVANT_SUBJECT}}`, `{{SERVICE}}`,
`{{THE_SPECIFIC_STANDARD_THE_PARTNER_CARES_ABOUT}}`, `{{CONCRETE_TRUST_POINTS}}`,
`{{TANGIBLE_DELIVERABLE}}`, `{{CITY}}`, `{{INDUSTRY}}`, `{{THINGS}}`, `{{PATTERN}}`,
`{{RELEVANT_BEATS}}` — plus the short/long description code blocks and the directory
table.

### `gbp_posts.md` — queue entries
`{{OPERATIONAL_CHANGE_HEADLINE}}`, `{{PRICING_GUIDE_HEADLINE}}`,
`{{SEASONAL_ANGLE_HEADLINE}}`, `{{SLUG}}` — and the post body inside each code fence.

### `todo.md`
Replace all four example items with your real deferred tasks.

---

## Final check

Nothing real is filled in until this returns nothing:

```sh
grep -rn '{{' docs/        # any leftover global token
grep -rn '_[a-z].*_' docs/ # rough check for leftover italic prompts (expect some false hits)
```
