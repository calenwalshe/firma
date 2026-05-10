---
layer: foundation
status: stable
last_reviewed: {{LAUNCH_DATE}}
review_cadence: quarterly
---

# {{COMPANY_NAME}} — Charter

This is the document everything else in this company must be consistent
with. Edits require an ADR (`decisions/`).

---

## Definition

{{COMPANY_NAME}} is {{ONE_LINE_PURPOSE}}.

It is a {{LEGAL_SHAPE}}, formed in {{STATE_OF_FORMATION}} on {{LAUNCH_DATE}}.

---

## Why it exists

Two paragraphs of plain language. Not a mission statement; a real
answer to "why are we doing this?"

Paragraph 1 — what's the problem we're addressing? Who has it? Why is
the status quo not working?

Paragraph 2 — why is this company (this team, this timeline, this
surface) the right shape to address it?

(Replace these two paragraphs with the real answers.)

---

## What it is

1. **Concretely.** ({{e.g. "A family-law firm serving the Chicago metro."}})
2. **Structurally.** ({{e.g. "An Illinois LLP, three partners, one
   paralegal, one shared office."}})
3. **Strategically.** ({{e.g. "A boutique that competes on
   responsiveness and depth, not volume."}})

## What it is not

1. Not {{NEGATION_1}}. (e.g. "Not a high-volume mill.")
2. Not {{NEGATION_2}}. (e.g. "Not a generalist firm.")
3. Not {{NEGATION_3}}. (e.g. "Not pursuing class-action work.")

The "what it is not" list is load-bearing. It names the most-tempting
drift directions and rules them out before they happen.

---

## Who it serves

- {{AUDIENCE_1}} — one line.
- {{AUDIENCE_2}} — one line.
- {{AUDIENCE_3}} — one line.

(2–4 audiences. Specific. No "businesses of all sizes." If your
audience reads as "anyone with a credit card," you haven't named your
audience yet.)

---

## Brand stance

The default: the company's brand is its own. Founder names appear
publicly if appropriate to the field — lawyers, doctors, consultants,
service providers usually yes; product companies usually no.

(Edit to the real stance.)

If your brand stance is "founder behind brand" (the founder doesn't
appear publicly — for example, the founder has a day job that creates
a conflict, or the founder is building stealth-from-an-employer), say
so explicitly here and add an ADR documenting why.

---

## Sunset

This company has a sunset condition. Pick one of:

- **Time-bound:** wind down on or before {{SUNSET_DATE}}.
- **Outcome-bound:** wind down if {{SUNSET_OUTCOME}} is not met by
  {{SUNSET_CHECK_DATE}}.
- **Disprove-bound (90-day default for pre-revenue):** the company
  closes on {{LAUNCH_DATE + 90 days}} unless one of these has happened:
  - {{First paying customer signed.}}
  - {{First contracted output delivered to a real outside party.}}
  - {{Quantitative signal that the disprove condition was wrong; if
    so, draft a new CHARTER and reset the clock — recorded as ADR.}}

If this company genuinely should not have a sunset (an established,
revenue-generating going concern; a multigenerational family business),
delete this section AND record the reasoning in
`decisions/0001-founding.md` § Sunset.

The sunset is the forcing function. A company without a forcing
function tends to drift.

---

## Constraints (always live)

5–10 constraints that this company commits to upfront. These are
load-bearing — every operational decision must be consistent with
them.

(Edit. Common shapes:)

1. {{CONSTRAINT_1}}
2. {{CONSTRAINT_2}}
3. {{CONSTRAINT_3}}

Examples (don't copy; replace with your own):

- "No work for clients in regulated industries until counsel reviews
  the engagement letter."
- "No public marketing until brand identity finalized."
- "No taking outside investment in year 1."
- "No contractor work without a signed IP-assignment in place first."
- "No founder-personal-leverage on customer calls until the company
  has its own track record."

---

## What this document is

The CHARTER. Edits require an ADR. If you find yourself wanting to
edit it often, the company's shape is wrong — name what changed and
why in an ADR.
