<!--
TEMPLATE — genericized from a real client project's docs/citations.md.
Placeholders: {{BUSINESS_NAME}} {{LEGAL_NAME}} {{REG_NUMBER}} {{ADDRESS}} {{PHONE}}
{{EMAIL}} {{DOMAIN}} {{HOURS}} {{LOGO_URL}} {{PRIMARY_CATEGORY}} {{SERVICE_AREA}}
Directory names below are examples — swap for the ones that carry weight in your country.
-->

# Off-site authority — citations, partnerships, PR

The work that lives **outside** the codebase: directory citations, referral
partnerships, digital PR. For a local business this moves the ranking needle more than
any on-page change once the on-page work is done — external validation is a signal no
amount of your own schema can substitute for.

**The agent can't do this part.** Signup needs email/phone verification (and sometimes a
document upload) the business owner controls. Everything below is prepped so each one is
a five-minute copy-paste, not a from-scratch write.

## Canonical NAP — use this exact block everywhere

Citations only help if they're **consistent**. A mismatched address or phone format
across listings actively hurts local ranking. Paste this verbatim into every profile;
don't reformat per-platform.

```
Business name:      {{BUSINESS_NAME}}
Legal name:         {{LEGAL_NAME}} (Reg. {{REG_NUMBER}})
Address:            {{ADDRESS}}
Phone:             {{PHONE}}
Email:              {{EMAIL}}
Website:           https://{{DOMAIN}}
Hours:             {{HOURS}}
Logo/profile photo: {{LOGO_URL}}
```

**Categories:** Primary — {{PRIMARY_CATEGORY}}. Secondary (where allowed) — list 2–3
closest matches.
**Service area:** {{SERVICE_AREA}}.

### Short description (~150 chars — social bios, GBP short description)
```
{{ONE_SENTENCE_WHAT_YOU_DO_WHERE_AND_THE_MAIN_TRUST_POINT}}
```

### Long description (~700 chars — review-site bios, "About" sections)
```
{{2-4 SENTENCES: legal name + registration, what you do, the full service list, the
area, and the concrete trust mechanism — upfront pricing, free inspection, guarantee.}}
```

## Directory claims

For each: search for an existing (possibly auto-created) listing first and **claim it**
rather than making a duplicate. Verify via the business email or a phone OTP. Once live,
send the profile URL to whoever maintains the site so it gets added to `sameAs` in the
`LocalBusiness` schema — **that's what turns a listing into a ranking signal** instead
of just a page that exists.

| Directory | Why it matters | Status | Date |
|---|---|---|---|
| Main national review platform | Carries local weight; partners check it before referring | Not claimed | — |
| Facebook Business Page | Real `sameAs` entity + a place to cross-post GBP updates | Not claimed | — |
| Bing Places | Feeds Bing's local index — which AI search/browsing leans on | Not claimed | — |

Tip: if Bing Places offers to import from an already-verified Google Business Profile,
use it — instant verification and no manual re-entry.

## Partnership outreach (referral + backlink channel)

For businesses whose customers are the exact people who need your service (e.g. letting
agents for end-of-tenancy cleaning). A link from even 3–4 partner sites' "recommended
suppliers" page is a strong local signal, not just a referral source.

```
Subject: {{PARTNER_RELEVANT_SUBJECT}}

Hi [Name],

I run {{BUSINESS_NAME}} — we do {{SERVICE}} across {{AREA}}, and a big part of what we
focus on is {{THE_SPECIFIC_STANDARD_THE_PARTNER_CARES_ABOUT}}.

We're {{CONCRETE_TRUST_POINTS}}, and every job gets {{TANGIBLE_DELIVERABLE}}. Happy to
do a free walkthrough on a current job so you can see the standard directly, and we're
open to a standing referral arrangement if that's useful.

Worth a quick call this week?

[Name] · {{BUSINESS_NAME}} · {{PHONE}} · {{EMAIL}}
```

**Where to send it:** search "[partner type] [suburb]" for the 4–5 highest-volume
suburbs in your service area.

## Digital PR — local press pitch

A non-promotional hook beats a company announcement. If you publish real pricing, you
have data a journalist can cite.

```
Subject: Local data — what {{SERVICE}} actually costs in {{CITY}} right now

Hi [Journalist],

I run a {{INDUSTRY}} business in {{AREA}} and we publish real pricing rather than
"request a quote" — so we have actual booking data on what {{THINGS}} cost across
different {{CITY}} suburbs, and which areas see the most {{PATTERN}}.

If you ever cover {{RELEVANT_BEATS}}, happy to share the real numbers — no pitch, just
data if it's useful.

[Name] · {{BUSINESS_NAME}}
```

**Where to send it:** city hyperlocal outlets, the community edition covering your
suburb, or a freelance journalist on the relevant beat.

## Status

| Channel | Status | Date |
|---|---|---|
| Review platform | Not claimed | — |
| Facebook Business Page | Not claimed | — |
| Bing Places | Not claimed | — |
| Partnership outreach | Not started | — |
| Digital PR pitch | Not started | — |

Update this table as each goes live, and feed the profile URLs back into the site's
`sameAs` schema.
