---
layer: team
status: template
---

# Team — Hiring, roles, IP-assignment

The team layer answers: who works here, what do they do, and how is
IP assigned and protected.

For solopreneurs committed to staying solo: you can delete this layer.
Delete the `60-team/` directory and the `decisions/0001-founding.md`
will record that the company is single-operator-by-design.

For everyone else: read on.

---

## Roles at v0

A real company has 1-3 roles at v0. Adding more roles before there's
revenue creates ceremony.

### Founder / director

- **Name:** {{FOUNDER_NAME}}
- **Owns:** kill-or-keep call, inheritance posture, ADR authorship,
  customer-segment definition, pricing, vendor selection, hiring (if
  any). The founder is the single named person on every external
  contract until that responsibility is delegated.
- **Compensation:** founder draws (LLC / sole-prop) or W-2 salary
  (corp, including S-elected LLC) per
  [`20-financial/README.md`](../20-financial/README.md).

### Co-founder(s) (if any)

- **Names:** {{CO_FOUNDER_1, CO_FOUNDER_2, ...}}
- **Equity split:** named in operating agreement / partnership
  agreement / bylaws. Common splits: equal among 2–3 co-founders;
  weighted (e.g. 60/40, 50/30/20) when contributions or risks differ.
- **Vesting:** standard is 4-year vest with 1-year cliff. If you
  haven't formalized this, do it before the company has any revenue
  — vesting agreements signed retroactively are awkward.
- **Roles:** name them. CEO / CTO / COO / Managing Partner / etc. If
  you can't decide, that's a decision worth recording in an ADR.

### First contractor (1099)

- **When:** as soon as the founder needs help with bounded work that
  isn't a full role. Typically: design, copywriting, accounting,
  legal, specific engineering tasks.
- **Required before any work:** signed contractor agreement INCLUDING
  IP-assignment language.
- **Don't skip the IP-assignment.** Without explicit assignment in
  writing, IP created by a contractor is **owned by the contractor**,
  not the company. This is the most common, most expensive mistake
  small companies make.

### First W-2 employee

- **When:** when the work is ongoing, the worker is integrated into
  the company's operations, and you're past the IRS contractor-vs-
  employee classification line.
- **Required before day 1:** offer letter, IP-assignment agreement,
  state-law-required new-hire paperwork (W-4, I-9, state withholding
  forms).
- **Setup:** payroll provider (Gusto / Justworks / OnPay / Rippling),
  workers' compensation insurance (state-mandated), unemployment
  insurance registration with your state.

W-2 vs 1099 is not a preference; it's a legal classification.
Misclassifying a W-2-shaped worker as a 1099 contractor is a federal
+ state penalty risk. The IRS publishes a 20-factor test; common
shorthand: do you control how the work is done (W-2) or only what
the deliverable is (1099)?

---

## What the seed does NOT have at v0

| Role | When it lands | Why not at v0 |
|---|---|---|
| Chief of Staff | When founder's read-throughput caps out | Sub-5-person teams route founder-direct |
| Marketing role | When you have an audience to talk to | At v0, the founder is the marketing |
| Compliance / legal officer | When regulatory burden justifies | At v0, IP and legal route through outside counsel |
| Engineering manager | When eng team is 4+ ICs | Until then, the founder or a senior IC manages |
| HR | When team is 15+ | Until then, the operations function or PEO covers HR-shaped tasks |

These are not banned. They land when they earn the seat. If you have
a reason to land one of them earlier, file an ADR explaining why
(e.g. "regulated industry; compliance officer required by license").

---

## IP-assignment posture (load-bearing)

Every person who creates IP for the company signs an IP-assignment.
Every. One.

- **Founders:** in the operating agreement / shareholders' agreement /
  partnership agreement.
- **Co-founders:** same.
- **Contractors:** in the contractor agreement (every engagement).
- **Employees:** in the offer letter / employment agreement.
- **Advisors:** in the advisor agreement (especially if they're
  giving substantive technical or product advice).

Things that count as "IP" for assignment purposes:

- Code (production, prototype, throwaway).
- Designs and brand assets.
- Written content (specs, marketing copy, blog posts).
- Trade secrets (process, methodology, customer lists).
- Inventions (provisional patents, trade-secret-protected mechanisms).

If a person creates something for the company without an IP-
assignment in place, the company doesn't own it. Fix this before
revenue, before any external IP filings, before any acquihire-or-
acquisition conversation.

---

## Equity (corps) and profits-interest (LLCs)

If you grant equity to non-founders:

- **C-corp:** typically Incentive Stock Options (ISOs) for employees,
  Non-Qualified Stock Options (NSOs) for advisors and contractors.
  Restricted Stock Units (RSUs) at later stages. **Requires a 409A
  valuation** before any grant — get one before grants. Carta and
  Pulley handle 409As (~$1,000–$3,000) and the ongoing cap table.
- **LLC:** profits-interest grants (preferred over membership-
  interest grants for tax reasons). Requires a vesting schedule and
  in many cases an 83(b) election filed within 30 days of grant.
  Talk to a CPA before the first grant.

Don't try to DIY equity grants. Use Carta / Pulley or attorney-drafted
documents. The cost of getting this wrong is much larger than the
cost of doing it right.

---

## Onboarding pattern

When the first hire (any shape) joins:

1. Sign the agreement before any work begins.
2. Set up access (email, code repository if relevant, shared docs).
3. Walk through the company's CHARTER, PRINCIPLES, and recent ADRs.
4. Name the first 30-day deliverable in writing.
5. First week: light schedule, biased toward learning, not output.
6. First month: documented check-in on shape-fit and direction.

This is not an HR program. It's a 30-minute checklist the founder
runs once for every new person.

---

## What this layer is NOT

- A full employee handbook. (Lives in
  `60-team/employee-handbook-skeleton.md` when you graduate the layer.)
- A performance-management framework. (Build when you have to.)
- A DEI policy or anti-harassment training. (You'll need these at
  scale; deferred until they apply.)

---

## Graduation path

```
60-team/
├── README.md
├── first-hire-framework.md      # decision tree: when, who, what role
├── role-template.md             # role definition shape
├── equity-grant-template.md     # ISO/NSO/RSU/profits-interest pointers
├── ip-assignment-template.md    # standalone IP-assignment doc
└── employee-handbook-skeleton.md
```

Add as you earn it.
