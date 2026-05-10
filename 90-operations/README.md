---
layer: operations
status: template
---

# Operations — Vendors, insurance, compliance, IR

The operations layer answers: what infrastructure does the company
depend on, what insurance protects it, what regulations apply, and
what happens when something goes wrong.

---

## Vendor register

Keep a list of every recurring vendor relationship. Fields:

- **Vendor.** Who.
- **What for.** Service / product.
- **Contract type.** Month-to-month / annual / multi-year.
- **Cost.** Monthly or annual.
- **Renewal date.** Calendar reminder ahead of this.
- **Cancellation path.** How long does it take to cancel; any
  early-termination penalties.
- **Owner.** Who at the company is accountable for this relationship.

Default shape (when you build a `vendor-register.md`):

```
| Vendor | What for | Cost | Renewal | Owner |
|---|---|---|---|---|
| Cloudflare | DNS + CDN | $0/mo | n/a | founder |
| Google Workspace | Email + docs | $7/user/mo | recurring | founder |
| Stripe | Payments | 2.9%+30¢/txn | n/a | founder |
| Mercury | Banking | $0/mo | n/a | founder |
| Northwest Registered Agent | RA service | $125/yr | YYYY-MM-DD | founder |
| {{vendor}} | {{purpose}} | {{cost}} | {{date}} | {{name}} |
```

When the register grows past ~10 vendors, add cancellation paths and
auto-renewal indicators. When it grows past ~20, graduate to a
dedicated vendor-management tool (Vanta, Tropic, Sastrify) — but
most companies sub-10 don't need that.

---

## Insurance

The right time to buy insurance is **before you need it**. The
moments to buy each kind:

### General Liability (GL)

- **When:** the moment you have any client-facing revenue.
- **Why:** covers third-party bodily injury and property damage.
  Standard requirement for most B2B contracts. Cheap (~$500–$1,500/yr
  for most small businesses).
- **Provider:** Hiscox, Next Insurance, The Hartford, Chubb. Online
  in 30 minutes.

### Errors and Omissions (E&O) / Professional Liability

- **When:** if you provide professional services (consulting,
  software development, advisory). Required by many enterprise
  customers' procurement processes.
- **Why:** covers damages from professional mistakes (a bug crashed
  the customer's site, your advice cost them money).
- **Cost:** ~$1,000–$3,000/yr for small consultancies.

### Cyber Liability

- **When:** if you store, process, or transmit customer data
  (especially PII, payment data, or healthcare data).
- **Why:** covers breach response costs, regulatory fines, customer
  notification, credit monitoring.
- **Cost:** ~$1,000–$5,000/yr for small businesses; scales with data
  volume and sensitivity.

### Workers' Compensation

- **When:** the moment you hire your first W-2 employee. **Required
  by state law in nearly every state** for any company with employees.
- **Cost:** varies by state and industry; ~$500–$3,000/yr per
  employee for low-risk roles.

### Directors & Officers (D&O)

- **When:** when you take outside investment, when you have an
  independent board, or when you have material liability exposure to
  founders personally.
- **Cost:** $5,000–$15,000/yr for early-stage startups.

### Employment Practices Liability (EPLI)

- **When:** when you have W-2 employees and want protection against
  wrongful-termination, harassment, or discrimination claims.
- **Cost:** $1,000–$3,000/yr.

Most small companies start with GL only, add E&O if professional
services, add Cyber if customer data, add Workers' Comp on first
hire. Other coverage lands as the company shape demands.

---

## Compliance

What applies depends entirely on your industry and jurisdiction. The
seed names the categories; you fill in the specifics.

### Privacy

If you collect any personal data (names, emails, IPs), you have
privacy obligations. Sketch:

- **Privacy policy on the website.** Required by GDPR (EU/UK), CCPA
  (California), PIPEDA (Canada), and increasingly by other state and
  federal laws. Required by Apple App Store and Google Play if you
  ship a mobile app.
- **Data Processing Agreement (DPA)** with vendors that handle
  customer data on your behalf (your hosting provider, your email
  provider, your analytics provider). Most major vendors offer
  click-through DPAs.
- **Subject Access Requests (SAR).** GDPR/CCPA give users the right
  to ask you what data you have on them. Have a process; for small
  companies it's "founder reads the request, runs a query in
  Postgres, replies in 30 days."

The seed deliberately does NOT ship a privacy-policy template at v0
— jurisdiction-specific. Common starting points:

- **iubenda** — paid generator (~$30/yr) for small businesses.
- **Termly** — similar.
- **Termsfeed** — similar.
- **A privacy attorney** — best when you have material data
  exposure.

### Terms of Service

Same caveat. If you have a website, app, or service, write terms
that govern use. Same generators above; same recommendation that
material exposure justifies an attorney.

### Industry-specific

- **HIPAA** if you handle Protected Health Information (PHI). BAAs
  required with every vendor that touches PHI.
- **PCI-DSS** if you handle credit-card data directly. Most companies
  avoid this by using Stripe / Square (the payment processor handles
  PCI, you handle a subset).
- **SOC 2** if you sell to enterprise customers who demand it.
  Typically needed at ~Series A or first enterprise deal. ~$10k–$50k
  for the first audit.
- **GDPR Article 27 representative** if you serve EU customers but
  aren't established in the EU. Typically ~$500–$2,000/yr.

### Annual filings

- **Annual report** to the state of formation (most states; varies).
- **Foreign-qualification renewals** in any state where you're
  registered as a foreign entity.
- **Federal tax return** every year regardless of whether you owe.
- **State tax return** in your home state and any state with nexus.

Calendar these. Missing the annual report can administratively
dissolve the company in some states.

---

## Incident response

When something breaks, what does the company do?

Sketch (build out as `incident-response.md` when this layer
graduates):

### Incident classes

- **Production outage** — customer-facing surface is down.
- **Data exposure** — unauthorized access to customer data; possible
  breach.
- **Financial fraud** — banking breach; unauthorized charges.
- **Legal threat** — cease-and-desist; demand letter; subpoena.
- **Operational disruption** — key vendor outage; key employee
  unavailable.

### Response shape

For each class:

1. **Detect.** How did we know.
2. **Triage.** What's the scope, who's affected.
3. **Mitigate.** Stop the bleeding.
4. **Communicate.** Customers, stakeholders, regulators (if required).
5. **Resolve.** Fix the root cause.
6. **Postmortem.** What happened, why, what we change.

For data-exposure incidents specifically: most US states have breach-
notification timelines (typically 30-60 days). You'll need legal
counsel involved early. Cyber liability insurance (above) typically
includes breach-coach hours — use them.

---

## What this layer is NOT

- A full GRC (governance, risk, compliance) program.
- A security framework (lives separately if you build one out).
- A DR / BCP (disaster recovery / business continuity) plan.

The seed names the categories and the load-bearing checkpoints. It
does not write your full operations playbook.

---

## Graduation path

```
90-operations/
├── README.md
├── vendor-register.md
├── insurance-checklist.md
├── compliance/
│   ├── privacy-policy-template.md
│   ├── terms-template.md
│   └── data-handling.md
└── incident-response.md
```

Add as you earn it.
