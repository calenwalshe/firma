---
layer: foundation
status: template
---

# Operating Principles — {{COMPANY_NAME}}

5–10 principles that guide how decisions get made when no one's
looking. Concrete and testable. Not aspirational marketing copy.

---

## Template — keep, fork, or replace

The seed ships these as starter principles. Most companies should keep
3–4 of them and write their own for the rest. The named principle
should fit the company's actual posture, not borrow generically.

### 1. Do the obvious thing first

If a customer / employee / partner can guess what we'd do in a given
situation and they're right, we're doing the right thing. Surprises in
small things signal noise; we keep the small things consistent.

### 2. Default to writing things down

If a decision was discussed but not written, it didn't happen. ADRs in
`decisions/` are the only durable record. Slack / email / meetings are
ephemeral.

### 3. Customers are not adversaries

Pricing, contracts, and disputes assume the customer is acting in good
faith until proven otherwise. We refund quickly. We say no clearly. We
don't bury fees.

### 4. Money runs the calendar

Cashflow drives priority, not vibes. Quarterly review of runway is
mandatory; if runway < 6 months without inbound, we're in survival
mode and act accordingly.

### 5. Slow is smooth, smooth is fast

Cutting corners on legal, financial, or compliance work creates
expensive backlog. We do these once, correctly. Speed comes from doing
the obvious thing without rework, not from skipping steps.

### 6. Hire for what we don't want to do ourselves

The first hire is the role the founder is worst at AND most resents.
Hiring for "more of what I do well" delays the founder's own
bottleneck.

### 7. The website is a contract

Public claims are commitments. We don't claim certifications we don't
have, capacities we can't deliver, or testimonials we can't
substantiate.

### 8. Disagreement is logged, not litigated

Hard calls get written up as ADRs with the dissenting view recorded.
A no-vote in writing is preserved; a no-vote in argument is forgotten.

---

## Editing this file

Edits require an ADR. If you change a principle, the ADR records the
old principle, the new one, and what triggered the change.

- **Adding a principle:** append-only. Number it.
- **Removing a principle:** ADR explicitly. Don't quietly delete — a
  removed principle is information about how the company evolved.
- **Replacing a principle:** new ADR; old principle quoted in the
  ADR's Context section.

---

## What this document is not

- Not a values statement. Values are aspirational; principles are
  testable.
- Not a code of conduct (that's an HR doc, lives in
  `60-team/employee-handbook-skeleton.md` if you have one).
- Not a customer-facing pitch. These are for the people running the
  company.
