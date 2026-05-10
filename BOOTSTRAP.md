# BOOTSTRAP — Setup / First use / Ongoing

Read this once, end-to-end, before touching anything. ~15 minutes.

This is the setup runbook for a new workspace starting from this
scaffold. It walks **Setup** (decisions and structure), **First use**
(making the scaffold yours), and **Ongoing** (how it gets used over
time).

The scaffold is shape-neutral: it works for a research project, a
freelance practice, a multi-collaborator engineering effort, a small
operation with several moving parts, or anything else with enough
complexity that decisions need tracking and context needs preserving.
Where this runbook gives concrete examples (banks, EINs, registered
agents) those apply to the workspaces that need them; skip the sections
that don't fit your shape.

> **Not legal, financial, or tax advice.** For high-stakes decisions
> in any specific domain, retain the relevant professional.

---

## Before you start

Have ready:

- **Working name** for the workspace. Placeholder is fine; you can
  rename later. (The scaffold's tokens are all `{{COMPANY_NAME}}` —
  find/replace is a one-line shell command when you commit to a real
  name. The token is named `{{COMPANY_NAME}}` for historical reasons;
  it's the workspace name, whatever shape that workspace takes.)
- **One-line description.** "We do *what* for *whom*" — or for a
  research workspace, "investigating *what* about *what*."
- **Shape** picked: solo / partnership / small team / formal entity.
  If a formal entity is in scope, read [`10-legal/README.md`](10-legal/README.md)
  first.
- **A sunset shape** picked: 90-day disprove clock by default for
  pre-result workspaces; explicit "no sunset, here's why" in the
  founding ADR for established / ongoing work.

You do **not** need yet: a final brand, a logo, a website, hires,
customers, capital. The scaffold is for setup. Those land in first
use, ongoing, or later — for the workspaces that need them.

---

## Setup (about half a day)

### 1. Fork the scaffold

```bash
gh repo create my-workspace --template <seed-repo-url> --private
git clone git@github.com:<you>/my-workspace.git
cd my-workspace
```

Or copy the directory and `git init` from scratch.

### 2. The kernel is already vendored

The R&D layer ships inside this repo at [`_kernel/`](_kernel/). No
submodule init step, no external fetch — the kernel travels with the
scaffold.

You don't need the kernel on day one. You need it the first time you
want to investigate a hard question methodically (a new market, a
pricing experiment, a technical bet, a research question). When you
do, see [`_kernel/README.md`](_kernel/README.md).

If you'd rather strip the kernel out (you genuinely have no
investigation work to do, or you want to swap in a different R&D
layer), delete the `_kernel/` directory and record the removal as an
ADR.

### 3. Find-and-replace placeholder tokens

Every template carries `{{TOKENS}}`. The common ones:

| Token | Example |
|---|---|
| `{{COMPANY_NAME}}` | `Northbridge Family Law` / `Carmacks Geochemistry` / `Side Build Q3` |
| `{{COMPANY_SLUG}}` | `northbridge` / `carmacks` / `q3-build` |
| `{{LAUNCH_DATE}}` | `2026-05-10` |
| `{{LEGAL_SHAPE}}` | `LLP` / `n/a — informal research workspace` |
| `{{STATE_OF_FORMATION}}` | `Illinois` / `n/a` |
| `{{FOUNDER_NAMES}}` | `Alex Kim, Sara Patel` |
| `{{ONE_LINE_PURPOSE}}` | `Family-law representation for the Chicago metro.` / `Investigating the petrogenesis of the Carmacks volcanic group.` |
| `{{REGISTERED_AGENT}}` | `Northwest Registered Agent` |
| `{{DOMAIN}}` | `northbridgefamilylaw.com` |

To see every unfilled token in your repo:

```bash
grep -r "{{" . --exclude-dir=.git --exclude-dir=_kernel
```

When that returns nothing, the scaffold is filled.

### 4. Delete layers that don't apply

The scaffold ships nine layer directories. Most workspaces don't need
all nine on day one:

- **No product surface?** Delete `80-product/`. Add it back if you
  ever ship one.
- **Solo?** Delete `60-team/`. Add it back if the picture changes.
- **No revenue?** Keep `70-sales/` but expect it to be mostly empty
  for a while, or delete it entirely for non-revenue workspaces.
- **No counterparties?** Keep `40-comms/`; just fill in the
  "internal" subsection and leave the rest as TBD.
- **No formal entity?** Most of `10-legal/` and `90-operations/` can
  be deleted.

Don't keep layer directories you genuinely don't have content for —
they read as ceremony.

### 5. (If applicable) Pick a formal shape and run formation

If the workspace is a formal entity, open
[`10-legal/README.md`](10-legal/README.md). Pick:

- **LLC** — most common; good liability shield + pass-through tax.
- **C-corp** — required for most VC-funded structures. Delaware default.
- **LLP** — for licensed professional services.
- **Sole-prop / DBA** — fastest; no liability shield. Convert later.

Most shapes: ~$300 + 1–7 days end-to-end. For workspaces that don't
need a formal entity (informal research, a side build, an internal
investigation), skip this entire step.

### 6. (If applicable) EIN

If the workspace is a US formal entity, apply for an EIN at
[irs.gov](https://www.irs.gov/businesses/small-businesses-self-employed/apply-for-an-employer-identification-number-ein-online)
after formation papers come back. Online filing takes ~15 minutes; EIN
issued same day for most US-based filers.

### 7. Sign the founding ADR

Open [`decisions/0001-founding.md`](decisions/0001-founding.md). It's
prefilled with the common shape; fill in the workspace-specific
reasoning. Date it. The founding ADR is the workspace's contract with
itself — the first entry in the decision log that explains why this
exists.

### 8. First commit

```bash
git add .
git commit -m "feat: bootstrap {{COMPANY_SLUG}}"
```

That's setup. You have a workspace with structure, a written record
of why it exists, and (if applicable) a legal entity in flight.

---

## First use (about a half-day, spread across 3–5 days)

### 9. (If applicable) Bank account

Read the picks in [`20-financial/README.md`](20-financial/README.md).
Defaults:

- **Mercury** for tech / SaaS / online workspaces — opens online in
  2–4 days for most US LLCs and corps.
- **Bluevine** for service practices wanting free checking.
- **A local bank** for workspaces with cash deposits, in-person
  needs, or where Mercury/Bluevine don't fit.

Skip entirely if the workspace doesn't handle money.

### 10. Domain + email

Read [`30-brand/README.md`](30-brand/README.md). Defaults:

- **Domain registrar:** Cloudflare Registrar. ~$10/yr for `.com`,
  no upsell.
- **Email:** Google Workspace ($7/user/month) for most; FastMail
  ($5/user/month) for privacy-leaning workspaces; Microsoft 365 if
  you're already deep in the Office ecosystem.

You should have `<you>@<domain>` working by end of first-use week, if
the workspace has an external face.

### 11. Bookkeeping

Set up books, if relevant. Defaults:

- **Wave** (free) at solo scale.
- **QuickBooks Online** ($30+/month) when income is material or
  you've hired a CPA.

Basis (cash vs accrual): cash by default at setup; accrual when
revenue >$1M/yr or an investor demands it.

### 12. Comms posture

Open [`40-comms/README.md`](40-comms/README.md) and customize:

- **Internal:** at <5 people, email + in-person is enough. No Slack
  needed yet.
- **External:** a single-page website (the scaffold has a skeleton
  you can ship).
- **Counterparty:** a `help@` alias forwarding to the main inbox.
- **Inbound forms:** Tally or Typeform if you need lead capture.

### 13. Brand basics

If you have a brand picked, fill in `30-brand/README.md` § Visual
identity. If you don't, the scaffold ships a "no brand yet" placeholder
palette (warm-black + off-white + one accent; Inter sans + IBM Plex
Mono + Playfair Display) — usable for months while you decide.

---

## Ongoing (variable, as the workspace evolves)

### 14. First real result

This is where the scaffold steps back and the workspace actually
begins. What "first real result" looks like depends on the shape:

- **Service practice:** open a pipeline (`70-sales/README.md`), name
  the first 5 prospects, send the first proposal.
- **Product workspace:** ship the smallest counterparty-facing
  surface (`80-product/README.md`). Land a first paying customer or
  a first validated user.
- **Research workspace:** complete the first investigation cycle in
  `_kernel/`; record the result; decide whether the hypothesis
  holds.
- **Hybrid:** focus on the one that produces a result first. Don't
  run two motions until one is producing.

### 15. (If applicable) Insurance

Read [`90-operations/README.md`](90-operations/README.md) §Insurance.
Get General Liability the moment you have any counterparty-facing
revenue; add E&O for service practices; cyber if you handle
counterparty data.

### 16. The 90-day check-in

If you set a 90-day disprove clock at setup, day 90 is the forcing
date. Open the CHARTER's §Sunset section and answer honestly:

- **Did the disprove condition trip?** (revenue / customer / output
  / hypothesis)
- **Was the disprove condition wrong?** (you learned something the
  shape needs to change for; if so, write a new CHARTER and reset
  the clock — record this as an ADR.)
- **Did neither happen?** (close the workspace per
  [`00-foundation/CHARTER.md`](00-foundation/CHARTER.md) §Sunset.)

The forcing function only works if you actually run the check.

---

## What you now have

- A workspace with structure.
- A founding ADR explaining why it exists.
- An ADR log ready to record every subsequent decision.
- The layer scaffolding ready as the workspace grows into it.
- The R&D kernel ready as you need it.
- (If applicable) a legal entity, EIN, bank account, domain.

Total time to "real": ~1–2 weeks calendar, ~5–10 hours of operator
time spread across that span. Total spend: $0 for an informal
workspace; ~$300 formation + ~$30/year ongoing for a US formal
entity, plus tooling as needed.

---

## What you don't yet have

- **Counterparties.** Read [`70-sales/README.md`](70-sales/README.md).
- **A shippable surface** (if anything will ship). Read
  [`80-product/README.md`](80-product/README.md).
- **Insurance.** Read [`90-operations/README.md`](90-operations/README.md)
  §Insurance.
- **Collaborators.** Read [`60-team/README.md`](60-team/README.md)
  when it's time.
- **A privacy policy / terms.** Read
  [`90-operations/README.md`](90-operations/README.md) §Compliance.

The scaffold flags these as "do this when X" rather than "do this on
day one," so you don't drown in checklists you don't yet need.

---

## When NOT to use this scaffold

- **You're past 10 people on day one.** Fork to a fuller stack; the
  scaffold is sized for 1–10.
- **You're a regulated-industry workspace** (broker-dealer, fintech
  with deposit-taking, healthcare with PHI). The compliance shelf is
  starter-grade; you need industry-specific tooling and counsel.
- **You're institutionally-funded out of the gate.** The scaffold
  gets you to seed-stage ready; you'll need cap-table software, a
  proper 409A, and formal board governance — layer those on top.
- **You don't actually have a single shape yet.** If "what we do"
  reads as two efforts joined by "and", split or reduce scope before
  scaffolding. The scaffold is for one workspace doing one shape,
  not for exploring three.
