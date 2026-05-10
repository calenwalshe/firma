---
layer: financial
status: template
---

# Financial — Bank, books, taxes, runway

> **Not financial or tax advice.** For high-stakes calls (multi-state
> filings, equity events, regulated industries, foreign-source income),
> talk to a CPA.

---

## What this layer covers

- **Banking** — where the company's money sits.
- **Bookkeeping** — what records you keep and where.
- **Taxes** — what you owe and when.
- **Runway** — how long the money lasts at current burn.

The defaults below cover ~80% of small-company cases. The "when to
swap" notes mark the inflection points where the default stops fitting.

---

## Banking

| Provider | Best for | Notes |
|---|---|---|
| **Mercury** | tech / SaaS / online businesses | Free; opens online in 2–4 days for most US LLCs/corps; weak on cash deposits. |
| **Bluevine** | service firms | Free business checking; pays interest; opens online; weak on multi-user controls. |
| **Brex** | high-velocity B2B (SaaS, marketplaces) | Free; corporate-card-first; minimum revenue requirements. |
| **Local bank** | cash-handling, in-person needs, regulated | Slower account-opening; better for businesses depositing physical cash. |

**Default for a tech/online company:** Mercury.
**Default for a service firm wanting interest on idle cash:** Bluevine.
**Default for a business with cash deposits:** a local credit union or
community bank.

When to swap:
- You start handling cash → switch from Mercury to a local bank.
- You hit ~$5M in deposits → consider FDIC sweep (Mercury Vault and
  similar) or split across multiple banks for full FDIC coverage.
- You start moving real money internationally (>$50k/mo) → consider
  Wise Business or a bank with strong cross-border tooling on top of
  your primary.

**Required:** EIN before you open a business bank account. SSN-only
sole-prop accounts exist but you should use an EIN.

---

## Bookkeeping

| Software | Cost | Best for |
|---|---|---|
| **Wave** | free | Solopreneur / earliest stage |
| **QuickBooks Online** | $30+/mo | Anyone with a CPA, anyone past ~$100k revenue |
| **Xero** | $13+/mo | International or non-US-leaning founders |
| **FreshBooks** | $17+/mo | Service firms emphasizing invoicing |

**Default at founding:** Wave (free; pleasant interface; sufficient for
sole-props and small LLCs through year 1 typically).

**When to swap to QuickBooks Online:** when revenue clears ~$100k/yr,
when you bring on a bookkeeper, when you have material payroll, or
when you move from cash-basis to accrual.

### Cash vs accrual

- **Cash basis:** record income when received, expenses when paid.
  Default for most small companies. Simpler. Allowed for IRS purposes
  for most companies under $26M revenue.
- **Accrual basis:** record income when earned (invoiced), expenses
  when incurred. Required for: most C-corps with revenue >$26M;
  inventory-heavy businesses; companies with significant deferred
  revenue. Most VCs prefer to see accrual books.

**Default at founding:** cash basis.
**When to swap:** investor demands, $26M revenue, or significant
deferred-revenue contracts.

---

## Chart of accounts (sketch)

A starting chart for a small services or product company. Replace
account numbers with whatever your software uses by default; the
shape is what matters.

```
Assets (1xxx)
  1010  Operating bank account
  1020  Savings / sweep account
  1100  Accounts receivable
  1200  Prepaid expenses
  1500  Equipment

Liabilities (2xxx)
  2010  Accounts payable
  2050  Credit card payable
  2200  Sales tax payable (if you owe sales tax)
  2300  Accrued payroll (if you have W-2 employees)
  2500  Loans payable

Equity (3xxx)
  3010  Owner's equity / Common stock
  3020  Retained earnings
  3050  Owner draws (LLCs/sole-props) or Distributions

Revenue (4xxx)
  4010  Service revenue
  4020  Product revenue
  4050  Other income

Expenses (5xxx-6xxx)
  5010  Cost of goods sold
  6010  Rent
  6020  Software subscriptions
  6030  Professional fees (legal, accounting)
  6040  Travel
  6050  Marketing
  6060  Office supplies
  6100  Salaries and wages
  6110  Contractor payments (1099)
  6200  Bank fees
  6300  Insurance
```

You don't need all of these on day 1. Add as you earn them.

---

## Runway model

A simple monthly runway model (12-month sketch). Recommended structure
as a CSV / Sheet:

```
Month, Cash start, Revenue, Expenses, Cash end, Months runway
2026-05, $XX,XXX,    $X,XXX,  $X,XXX,   $XX,XXX,   X.X
...
```

At founding, fill in:
- **Cash start:** founder capital + any seed money.
- **Revenue:** zero or your first conservative estimate.
- **Expenses:** sum of every committed monthly expense (subscriptions,
  rent, contractors, etc.).

Quarterly review is non-negotiable. At every quarter:
- Update actuals.
- Re-forecast.
- If runway < 6 months without inbound, you're in survival mode —
  document this in an ADR and act accordingly.

---

## Taxes

### Federal

- **Income tax:** filed annually. Sole-prop on Schedule C; LLCs as
  default partnership (1065) or single-member-as-disregarded (Schedule
  C); C-corps file 1120; S-elections file 1120-S.
- **Self-employment tax:** sole-props and LLC members owe 15.3% on
  net earnings (Social Security + Medicare). S-corp election lets you
  split this between W-2 salary and distributions.
- **Quarterly estimated payments:** if you'll owe >$1,000 federal,
  the IRS wants quarterly estimated payments (Apr 15, Jun 15, Sep 15,
  Jan 15). Underpayment penalty if you skip.

### State

Varies. Common shapes:

- **Pass-through state income tax** (most states): your share of
  business income flows to your personal state return.
- **Franchise tax / annual report fee:** most states charge an annual
  fee for LLC/corp existence. Range: $0 (no fee) to $800 (California)
  to ~$25,000 in extreme cases (Delaware C-corp with high authorized
  shares — though most companies pay $300-$500).
- **Sales tax:** if you sell physical products or certain services,
  you may need to register for sales tax in your home state and any
  state where you have "nexus" (physical or economic). Wayfair v.
  South Dakota (2018) made economic nexus standard — typically $100k
  revenue or 200 transactions per state per year.

### Local

Some cities (Seattle, San Francisco, NYC) have city-level business
taxes. Check.

### Tax-prep approach

- **DIY** for sole-props with simple finances and Schedule C — TurboTax
  Self-Employed handles it.
- **CPA** once you have an LLC/corp, employees, multi-state operations,
  or revenue past ~$100k. Expect $1,000–$3,000/yr for prep.
- **Bookkeeper + CPA** once you're past ~$500k revenue or have
  payroll. Bookkeeper does monthly closes; CPA does taxes.

---

## Payroll

You don't need this until you hire your first W-2 employee. Contractors
(1099) are paid out of the bank account directly and reported on a
1099-NEC at year-end.

When you do hire W-2:

- **Gusto** ($40+/mo + per-employee). Default for most small companies.
  Handles federal/state withholding, W-2s, healthcare benefits if you
  add them.
- **Justworks** (PEO; $80+/employee/mo). Simpler benefits + co-employer
  model; useful when hiring across multiple states early.
- **OnPay, Rippling** — alternatives at similar price points.

---

## Expense policy

A short, written expense policy at founding saves arguments later.
Sketch:

- Owner / founder draws or salary (per legal shape).
- Reimbursable expenses: list categories (travel, software, meals
  with clients).
- Non-reimbursable: personal items, alcohol unless directly
  client-facing, etc.
- Approval threshold: $X requires written approval (founder / partner
  / CFO depending on stage).
- Receipt retention: keep receipts >$75 (IRS minimum); 7 years
  retention for tax records.

---

## What this layer does NOT do

- Investment tax planning.
- International transfer pricing.
- Crypto / digital-asset tax handling (specialized; talk to a
  crypto-aware CPA).
- ESPP / stock-comp planning.
- M&A diligence prep.

---

## Graduation path

When this README outgrows one file:

```
20-financial/
├── README.md
├── bank-account-checklist.md
├── bookkeeping-stance.md
├── chart-of-accounts.md
├── runway-model.csv
├── expense-policy.md
├── taxes-checklist.md
└── payroll-setup.md
```

Add as you earn it.
