# BOOTSTRAP — Day 0 / Week 1 / Month 1

Read this once, end-to-end, before touching anything. ~15 minutes.

This is the spinup runbook for a new company starting from this seed.
It walks Day 0 (decisions and filings), Week 1 (banking, domain,
comms), and Month 1 (first customer or first ship-shape product surface).

> **Not legal, financial, or tax advice.** For high-stakes decisions
> (raising capital, hiring W-2 employees in multiple states, regulated
> industries, IP licensing), retain counsel.

---

## Before you start

Have ready:

- **Working name** for the company. Placeholder is fine; you can rename
  later. (The seed's tokens are all `{{COMPANY_NAME}}` — find/replace
  is a one-line shell command when you commit to a real name.)
- **One-line description.** "We do *what* for *whom*."
- **Legal shape** picked: LLC / C-corp / LLP / sole-prop. If unsure,
  read [`10-legal/README.md`](10-legal/README.md) first.
- **State of formation.** Default: your home state. Wyoming and
  Delaware have specific advantages — see `10-legal/README.md`.
- **A founder bank candidate.** Mercury / Bluevine / a local bank.
- **A sunset shape** picked: 90-day disprove clock by default for
  pre-revenue ventures; explicit "no sunset, here's why" in the
  founding ADR for established-revenue ventures.

You do **not** need yet: a final brand, a logo, a website, employees,
customers, capital. The seed is for day 0. Those land in week 1, month
1, or later.

---

## Day 0 (about half a day of founder time)

### 1. Fork the template

```bash
gh repo create my-company --template <seed-repo-url> --private
git clone git@github.com:<you>/my-company.git
cd my-company
```

Or copy the directory and `git init` from scratch.

### 2. The kernel is already vendored

The R&D layer ships inside this repo at [`_kernel/`](_kernel/). No
submodule init step, no external fetch — the kernel travels with the
seed.

You don't need the kernel on day 0. You need it the first time you
want to investigate a hard question methodically (a new market, a
pricing experiment, a technical bet). When you do, see
[`_kernel/README.md`](_kernel/README.md).

If you'd rather strip the kernel out (you genuinely have no investigation
work to do, or you want to swap in a different R&D layer), delete the
`_kernel/` directory and record the removal as an ADR.

### 3. Find-and-replace placeholder tokens

Every template carries `{{TOKENS}}`. The common ones:

| Token | Example |
|---|---|
| `{{COMPANY_NAME}}` | `Northbridge Family Law` |
| `{{COMPANY_SLUG}}` | `northbridge` |
| `{{LAUNCH_DATE}}` | `2026-05-10` |
| `{{LEGAL_SHAPE}}` | `LLP` |
| `{{STATE_OF_FORMATION}}` | `Illinois` |
| `{{FOUNDER_NAMES}}` | `Alex Kim, Sara Patel, Diego Reyes` |
| `{{ONE_LINE_PURPOSE}}` | `Family-law representation for the Chicago metro.` |
| `{{REGISTERED_AGENT}}` | `Northwest Registered Agent` |
| `{{DOMAIN}}` | `northbridgefamilylaw.com` |

To see every unfilled token in your repo:

```bash
grep -r "{{" . --exclude-dir=.git --exclude-dir=_kernel
```

When that returns nothing, the seed is filled.

### 4. Delete layers that don't apply

The seed ships nine layer directories. Most companies don't need all
nine on day 0:

- **Pure service firm with no product?** Delete `80-product/`. Add it
  back if you ever ship one.
- **Solopreneur who'll never hire?** Delete `60-team/`. Add it back if
  the picture changes.
- **Internal-only or pre-revenue?** Keep `70-sales/` but expect it to
  be mostly empty for a while.
- **No customer-facing comms surface yet?** Keep `40-comms/`; just fill
  in the "internal" subsection and leave the rest as TBD.

Don't keep layer directories you genuinely don't have content for —
they read as ceremony.

### 5. Pick legal shape and run formation

Open [`10-legal/README.md`](10-legal/README.md). Pick:

- **LLC** — most common; good liability shield + pass-through tax.
  Default for most small companies. State-of-formation usually = home state.
- **C-corp** — required for most VC-funded startups. Delaware default.
- **LLP** — for licensed professional services (law, accounting,
  medicine, sometimes architecture).
- **Sole-prop / DBA** — fastest to start; no liability shield. Convert
  later if traction.

Most shapes: ~$300 + 1–7 days end-to-end. If you're using a registered
agent (recommended for LLC/corp/LLP), Northwest Registered Agent and
Harbor Compliance are sane defaults at ~$125/yr; some founders use the
registrar baked into their formation service (LegalZoom, ZenBusiness,
Stripe Atlas).

### 6. EIN

After formation papers come back from the state, apply for an EIN at
[irs.gov](https://www.irs.gov/businesses/small-businesses-self-employed/apply-for-an-employer-identification-number-ein-online).
Online filing takes ~15 minutes; EIN issued same day for most US-based
filers (some structures and foreign founders take longer).

### 7. Sign the founding ADR

Open [`decisions/0001-founding.md`](decisions/0001-founding.md). It's
prefilled with the common shape; fill in the venture-specific
reasoning. Date it. The founding ADR is the company's contract with
itself.

### 8. First commit

```bash
git add .
git commit -m "feat: bootstrap {{COMPANY_SLUG}}"
```

That's day 0. You have a legal entity (or one in flight) and a written
record of why you're doing this.

---

## Week 1 (about a half-day of founder time, spread across 3-5 days)

### 9. Bank account

Read the picks in [`20-financial/README.md`](20-financial/README.md).
Defaults:

- **Mercury** for tech / SaaS / online businesses — opens online in
  2–4 days for most US LLCs and corps.
- **Bluevine** for service firms wanting a free business checking.
- **A local bank** for businesses with cash deposits, in-person
  needs, or where Mercury/Bluevine don't fit (regulated industries,
  cash-handling, certain non-US founders).

### 10. Domain + email

Read [`30-brand/README.md`](30-brand/README.md). Defaults:

- **Domain registrar:** Cloudflare Registrar. ~$10/yr for `.com`,
  no upsell.
- **Email:** Google Workspace ($7/user/month) for most; FastMail
  ($5/user/month) for privacy-leaning founders; Microsoft 365 if
  you're already deep in the Office ecosystem.

You should have `<you>@<domain>` working by end of week 1.

### 11. Bookkeeping

Set up books. Defaults:

- **Wave** (free) at solopreneur scale.
- **QuickBooks Online** ($30+/month) when income is material or
  you've hired a CPA.

Basis (cash vs accrual): cash by default at founding; accrual when
revenue >$1M/yr or an investor demands it.

### 12. Comms posture

Open [`40-comms/README.md`](40-comms/README.md) and customize:

- **Internal:** at <5 people, email + in-person is enough. No Slack
  needed yet.
- **External:** a single-page website (the seed has a skeleton you
  can ship).
- **Customer:** a `help@` alias forwarding to the founder inbox.
- **Inbound forms:** Tally or Typeform if you need lead capture.

### 13. Brand basics

If you have a brand picked, fill in `30-brand/README.md` § Visual
identity. If you don't, the seed ships a "no brand yet" placeholder
palette (warm-black + off-white + one accent; Inter sans + IBM Plex
Mono + Playfair Display) — usable for months while you decide.

---

## Month 1 (variable founder time depending on shape)

### 14. First customer / first product surface

This is where the seed steps back and the company actually begins.
What "month 1" looks like depends on the shape:

- **Service firm:** open a pipeline (`70-sales/README.md`), name the
  first 5 prospects, send the first proposal.
- **Product company:** ship the smallest customer-facing surface
  (`80-product/README.md`). Land a first paying customer or a first
  validated user.
- **Hybrid (consulting + product):** focus on the cash-generating
  side first. Don't run two motions until one of them is paying.

### 15. Insurance (when revenue is real)

Read [`90-operations/README.md`](90-operations/README.md) §Insurance.
Get General Liability the moment you have any client-facing revenue;
add E&O (errors-and-omissions) for service firms; cyber if you handle
customer data.

### 16. The 90-day check-in

If you set a 90-day disprove clock at founding, day 90 is the forcing
date. Open the CHARTER's §Sunset section and answer honestly:

- **Did the disprove condition trip?** (revenue / customer / output)
- **Was the disprove condition wrong?** (you learned something the
  shape needs to change for; if so, write a new CHARTER and reset the
  clock — record this as an ADR.)
- **Did neither happen?** (close the company per
  [`00-foundation/CHARTER.md`](00-foundation/CHARTER.md) §Sunset.)

The forcing function only works if you actually run the check.

---

## What you now have

- A legal entity (or sole-prop / DBA filing) on file with the state.
- An EIN.
- A bank account (or one in-flight).
- A domain and an email.
- A repository of templates ready as you need them.
- An R&D kernel ready as you need it.
- An ADR documenting day-0 decisions.

That's a real company. Total time to "real": ~1–2 weeks calendar, ~5–10
hours founder-time spread across that span. Total spend: ~$300
formation + ~$30/year ongoing minimums (domain + bank fees) + bookkeeping
software when revenue is material.

---

## What you don't yet have

- **Customers.** Read [`70-sales/README.md`](70-sales/README.md).
- **A product** (if you're shipping one). Read [`80-product/README.md`](80-product/README.md).
- **Insurance.** Read [`90-operations/README.md`](90-operations/README.md)
  §Insurance.
- **Hires.** Read [`60-team/README.md`](60-team/README.md) when it's time.
- **A privacy policy / terms.** Read [`90-operations/README.md`](90-operations/README.md)
  §Compliance.

The seed flags these as "do this when X" rather than "do this on day 0,"
so you don't drown in checklists you don't yet need.

---

## When NOT to use this seed

- **You're past 10 employees on Day 0.** Fork to a fuller stack; the
  seed is sized for 1-10 people.
- **You're regulated-industry-only** (broker-dealer, fintech with
  deposit-taking, healthcare with PHI). The seed's compliance shelf
  is starter-grade; you need industry-specific counsel and tooling.
- **You're VC-funded out of the gate.** The seed gets you to seed-stage
  ready; you'll need cap-table software (Carta / Pulley), a proper
  409A, and formal board governance — layer those on top of the seed.
- **You don't actually have a single shape yet.** If "what we do"
  reads as two ventures joined by "and", split or reduce scope before
  scaffolding. The seed is for one company doing one shape, not for
  exploring three.
