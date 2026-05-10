---
layer: sales
status: template
---

# Sales — Pipeline, contracts, billing

The sales layer answers: who are the customers, where are they in the
buying motion, what do you send them, and how do they pay.

For pre-revenue companies: this layer is mostly empty for a while.
Don't pre-build a CRM if you have zero prospects.

---

## Pipeline (markdown CRM at v0)

The seed's default at v0 is **a markdown CRM**: one file per customer
or prospect, in `70-sales/customers/`. It looks like:

```
70-sales/customers/
├── _example.md            # the shape, copy this
├── acme-corp.md
├── beta-industries.md
└── chen-family-trust.md
```

Each customer file has:

- **Name + contact info.**
- **Status:** prospect / qualified / proposal-sent / closed-won /
  closed-lost / customer / churned.
- **Source:** how did this opportunity arrive? Inbound / referral /
  outbound / partner.
- **Notes:** running log of conversations, with dates.
- **Documents:** links to proposals, SOWs, contracts you've sent
  this customer.
- **Next step + owner + due date.**

Why markdown and not a CRM tool at v0?
- Pipeline of <50 prospects fits easily in markdown.
- Markdown is greppable, diffable, version-controlled, doesn't lock
  you into anyone's data model.
- The cost of a CRM tool isn't $/month — it's the time spent
  configuring fields and pipelines.

When to graduate to a real CRM:

- **HubSpot Free** — when pipeline is >50 active opportunities or
  when you want email tracking and form integrations. Free for the
  basics; paid for marketing automation.
- **Pipedrive / Close** — when you have a sales-led motion and
  pipeline shape matters more than marketing tooling.
- **Attio** — when you want a more flexible, modern primitive that
  isn't HubSpot-shaped.
- **Airtable** — for hybrid use cases where the data shape matters
  as much as the workflow.

Most companies run on markdown longer than they expect.

---

## Contracts and proposals

### Proposal

The customer-facing pitch document. For service businesses, this is
where most revenue is won or lost.

Default shape (when you build a `templates/proposal.md`):

1. **What you're proposing.** The shape of work in 1-2 paragraphs.
2. **What you're not proposing.** What's deliberately out of scope.
3. **Outcomes.** The thing the customer gets when this is done.
4. **Process.** How the work proceeds, in 3-5 phases.
5. **Timeline + price.** Specific. Not a range unless the work
   genuinely is unscoped (then call out what makes it unscoped).
6. **Terms.** Payment terms, what triggers a milestone, IP, kill-fee.
7. **Acceptance.** Signature block.

### Statement of Work (SOW)

Shorter than a proposal. Used after the relationship is established
when the customer wants additional work. Names the deliverable, the
timeline, and the price. Cross-references the master agreement.

### Master Service Agreement (MSA)

The umbrella contract for ongoing relationships. SOWs hang off the
MSA. Signed once; SOWs reference it.

For first customers: you typically don't need an MSA. The proposal
itself is the contract. MSA enters the picture for repeat-business
relationships.

### NDA (mutual or one-way)

Most early-stage conversations don't need an NDA. Customer-discovery
calls don't. Vendor pitches usually don't. Investor pitches almost
never.

When you do need one (sharing genuinely sensitive information with a
prospect or partner): use a template, modify sparingly. Mutual NDAs
are easier to negotiate than one-way; one-way NDAs are appropriate
when only one side is sharing the sensitive thing.

### What the seed does NOT ship at v0

The seed deliberately does not ship a contract template at v0 —
contracts are jurisdiction-specific and your industry's risk profile
matters. Common starting points:

- **Cooley GO** — free templates aimed at startups (corp-shaped, but
  many work for LLCs too).
- **Andrew Bosworth / Y Combinator** — SAFE notes (only for VC-style
  financing, not customer contracts).
- **Bonsai** — paid contract templates aimed at freelancers.
- **Your bar association's small-business resources page** — often
  has free state-specific templates for service-firm engagements.

For a first paying customer, paying an attorney $500–$1,500 to draft
a customer-facing master agreement is worthwhile insurance.

---

## Billing

### What software

- **Stripe** — default for online-first businesses. Card + ACH +
  wire + international. Free to start; ~2.9%+30¢ per card transaction.
- **Square** — default for in-person businesses (restaurants, salons,
  retail). Lower per-transaction cost on card-present.
- **FreshBooks / QuickBooks invoicing** — for service firms sending
  invoices to be paid by check or ACH.
- **Mercury invoicing** — if you bank with Mercury and want
  built-in invoicing.

Pick one. Don't run two.

### Billing shape

Pricing models, ordered by complexity:

1. **Fixed-fee project billing.** Easiest to scope, easiest to
   collect on. Default for service firms early.
2. **Hourly / time-and-materials.** Trades scope risk for billing
   complexity. Use when scope is genuinely unscoped or when the
   client demands it.
3. **Subscription (monthly / annual).** Recurring. Easy to scale
   accounting; harder to manage churn.
4. **Per-unit / per-API-call.** Usage-based. Requires good metering
   instrumentation; common for product companies.
5. **Retainer.** Monthly fee for access to the company; deliverables
   negotiated within the retainer.

Most businesses run one or two of these, not all five.

### Net-X terms

- **Net-30** — payment due 30 days after invoice. Industry norm for
  B2B service firms.
- **Net-15** or **Net-7** — faster; better for cashflow; some
  clients push back.
- **Due on receipt** — typically only enforceable for first
  engagements or one-time work.
- **Net-60 / Net-90** — large enterprise customers will often demand
  these. Negotiate them down or accept that revenue lags by 60-90
  days.

Late-payment terms (1-1.5%/month interest after 30 days late) are
common; most small businesses don't actually charge them but having
them in the contract helps when a payment dispute escalates.

---

## What this layer is NOT

- A marketing-automation playbook.
- A growth-hacking framework.
- A scripted sales cadence.

The seed names the posture and the tooling. It does not write your
sales motion.

---

## Graduation path

```
70-sales/
├── README.md
├── pipeline-template.md       # markdown CRM shape
├── customers/
│   ├── _example.md
│   └── <customer-1>.md
├── billing-stance.md          # Stripe/Square/FreshBooks pick
└── templates/
    ├── proposal.md
    ├── sow.md
    ├── msa.md
    └── invoice.md
```

Add as you earn it.
