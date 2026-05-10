---
layer: product
status: template
---

# Product — Spec, roadmap, release pattern

The product layer answers: what does the company make, how is the
shape decided, and how does it ship.

For pure service firms with no product: delete this layer.

For everyone else: read on.

---

## What's a product, for the seed's purposes

Anything the company **ships and supports** that exists independently
of the customer's specific engagement:

- A SaaS application.
- An installable software product.
- A physical good.
- A subscription content / data feed.
- A hosted API.
- A standardized service offering with a defined deliverable shape
  (a service productized).

A consulting engagement that's bespoke per-customer is **not** a
product, even if it's repeatable. That belongs in `70-sales/` (as a
billing-pattern) and in your operations runbooks.

---

## SPEC pattern

A spec is the document that describes what the product does and
doesn't do, before it's built.

Default shape (when you build a `SPEC-TEMPLATE.md`):

1. **What this is.** One paragraph. Plain.
2. **Who it's for.** One paragraph. Specific.
3. **Problem.** What is broken in the current world.
4. **Approach.** How we'll address it.
5. **Out of scope.** What this version explicitly doesn't cover.
6. **Constraints.** Technical, regulatory, time, budget.
7. **Success criteria.** What does "done" look like, measurably.
8. **Open questions.** What we don't yet know that we'll need to
   decide before shipping.

Keep specs short. ~1-3 pages each. A 20-page spec is a sign you're
specing too much at once — break it into smaller specs.

---

## Roadmap

A roadmap is **phase-shaped, not calendar-shaped**. Each phase has
entry criteria (what must be true to start) and exit criteria
(what must be true to be done). Calendar dates are illustrative.

Default shape (3-4 phases is typical):

### Phase 1 — Discovery / Validation

**Entry:** problem named, customer segment named.
**Exit:** at least one customer or potential customer has agreed
the problem is real and they'd pay for the proposed shape.

### Phase 2 — Build (smallest viable surface)

**Entry:** Phase 1 exit.
**Exit:** the smallest customer-facing surface is shippable.

### Phase 3 — Live (first real users)

**Entry:** Phase 2 exit; deployed to production; first user has
access.
**Exit:** first paying customer signed; first revenue collected;
first piece of customer feedback captured.

### Phase 4 — Iterate

**Entry:** Phase 3 exit.
**Exit:** depending on the company, this might be "first 10
customers", "first $10k MRR", or "first quarter of profitability".
Or this is the steady state.

If your company genuinely has a 5+ phase roadmap, you've either got
a complex product or you're over-planning. Default to 3-4 phases;
add more only when the work genuinely doesn't fit.

---

## Release pattern

How does a change get from "developer's machine" to "customer-facing"?

For a 1-person company shipping a SaaS:

1. **Local testing.** It works on the developer's machine.
2. **Staging deploy** (if you have one). Same code, isolated data.
3. **Production deploy.** Customer-facing.
4. **Release notes.** Even at 1-person scale, write down what changed.
   It's the customer-facing changelog and the company's memory.

The seed doesn't pick CI/CD tooling. GitHub Actions, GitLab CI,
CircleCI, Vercel/Netlify auto-deploys, hand-rolled deploy scripts
all work. Pick one and document the steps in a runbook.

For a service firm productizing a deliverable:

1. **Internal review.** Someone other than the maker reads it.
2. **Customer delivery.** Send it.
3. **Feedback capture.** What did they say back; what would you
   change next time.

---

## Feedback loop

How customer signal flows back into product:

- **Direct support tickets** — capture, tag by theme, review weekly.
- **Customer interviews** — schedule a few per quarter; record (with
  permission); review with the team.
- **Usage analytics** — minimum viable instrumentation: pageviews,
  active users, key event funnels.
- **Cancellation reasons** — every churned customer gets a one-question
  exit survey: "Why did you cancel?" Most won't answer; the ones who
  do are gold.

Keep this lightweight at v0. The trap is building a feedback-program
before you have feedback to feed it.

---

## Pricing decisions

A product company has to decide pricing. The seed doesn't pick for
you, but flags the most-common shapes:

- **Free + paid tier.** Default for SaaS targeting small users.
  Trades acquisition for monetization.
- **Free trial + paid only.** Default when there's no good free use
  case (e.g., enterprise tooling).
- **Pay-as-you-go.** Usage-based. Common for API products.
- **Premium / niche.** Higher price point, smaller market, deeper
  product. The opposite of the SaaS-default freemium pattern.

Major pricing changes get an ADR. "We changed the free tier limit" is
not an ADR-worthy event; "we deprecated the free tier" is.

---

## Versioning

Pick a versioning scheme:

- **SemVer (Major.Minor.Patch)** for SDKs, libraries, APIs that other
  people depend on.
- **CalVer (YYYY.MM.PATCH)** for products that ship continuously.
- **No version**, just dated release notes — fine for SaaS where
  there's no installed surface.

---

## What this layer is NOT

- A product-management framework. The seed names the shape, not the
  process.
- A backlog tool. (Use Linear, GitHub Issues, Jira, or a shared
  document — pick what fits.)
- A user-research playbook. (Build when you have to.)
- A growth-hacking guide.

---

## Graduation path

```
80-product/
├── README.md
├── SPEC-TEMPLATE.md
├── ROADMAP-TEMPLATE.md
├── release-process.md
└── feedback-loop.md
```

Add as you earn it.
