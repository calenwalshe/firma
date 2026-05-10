---
layer: legal
status: template
---

# Legal — Pick your shape

> **Not legal advice.** This is starter material. For high-stakes
> decisions (raising capital, hiring W-2 employees in multiple states,
> regulated industries, IP licensing), retain counsel.

---

## Picking a legal shape

| Shape | Best for | Liability shield | Pass-through tax | Setup cost | Time |
|---|---|---|---|---|---|
| **Sole-prop / DBA** | first revenue, low-risk solo | NO | yes (Schedule C) | $0–50 | same day |
| **LLC** | most companies <10 ppl | YES | yes | $100–500 | 1–7 days |
| **C-corp** | VC-funded, plan to issue equity broadly | YES | NO (corporate tax) | $500–1,500 | 3–10 days |
| **S-corp election** | LLC owners with W-2 salary, payroll-tax savings | (see LLC) | yes (with constraints) | (atop LLC) | filing change |
| **LLP** | licensed professional services (law, medicine, accounting) | YES (partner-shielded) | yes | $200–800 | 3–10 days |

---

## Quick rules of thumb

- **Sole-prop** if: solo, low-risk, want to start tomorrow, will
  convert later. Know that you have NO liability shield. Schedule C on
  your personal taxes.
- **LLC** if: you're not raising venture capital, you want a
  liability shield, and you want pass-through tax. Default for most
  small companies. Wyoming and Delaware are options if your home
  state's filing surface is bad; otherwise file in your home state.
- **C-corp** if: you plan to raise from VCs or issue equity to many
  employees. Delaware is the convention. Also consider it if you'll
  have significant retained earnings or want QSBS treatment (5-year
  hold for tax-favorable sale of qualified small-business stock).
- **S-corp election** is a tax election an LLC or corp can make later
  — not a separate entity. Talk to a CPA about whether this is right
  for you (typically once the business clears ~$50k–$80k/yr profit
  and you can pay yourself a "reasonable" W-2 salary).
- **LLP** if: you're in a licensed profession (law, medicine,
  accounting, sometimes architecture or engineering). Some states
  require it for these professions; some allow professional LLCs
  (PLLC) instead — check your state's bar / licensing board.

---

## State of formation

- **Default: your home state.** Where you actually operate. Simplest
  tax picture, simplest filing, no need for a foreign-qualification
  filing in your home state on top.
- **Wyoming** if: you want lowest annual fees ($60), strong privacy
  (no member-name disclosure on the public record), and you don't
  mind paying for a registered agent. Fine for IP-holding LLCs and
  remote-only operations. Note: if you live and work in California,
  forming in Wyoming doesn't avoid California's $800/yr franchise
  tax — California taxes companies that are "doing business" there
  regardless of formation state.
- **Delaware** if: you're a C-corp planning to raise venture capital.
  Lawyers and investors expect Delaware. Annual franchise tax: ~$300
  minimum, more for companies with significant authorized shares.
- **Nevada** for LLCs — historically privacy-friendly, but fees have
  crept up; Wyoming is usually preferable now.

---

## Day-1 essentials (regardless of shape)

### Registered agent

If you form an LLC, corp, or LLP, you need a registered agent — a
person or service authorized to receive legal mail on behalf of the
entity at a physical address in the state of formation.

Sane defaults:

- **Northwest Registered Agent.** ~$125/yr, no upselling, privacy-
  respecting (won't use your address as bait for spam mail).
- **Harbor Compliance.** ~$99/yr, multi-state if you operate in
  several.
- **The formation service's bundled agent.** LegalZoom, ZenBusiness,
  Stripe Atlas, etc. all bundle one. Fine but watch for the
  upsell-after-year-1 pattern (introductory rate jumps in year 2).

You can be your own registered agent if you have a physical address
in the state and don't mind your address appearing on the public
record. Most founders pay the $125 for privacy.

### EIN (Employer Identification Number)

The IRS-issued tax ID for the business. You need one to:
- Open a business bank account
- Hire employees
- File business taxes (other than as a single-member LLC reporting
  on a Schedule C)
- Establish business credit

Apply online at [irs.gov](https://www.irs.gov/businesses/small-businesses-self-employed/apply-for-an-employer-identification-number-ein-online).
Free. ~15 minutes. EIN issued same-day for most US-based filers (some
structures and foreign founders take longer).

If your formation paperwork hasn't returned yet, wait — the IRS
application asks for your formation date and entity type, and getting
those wrong creates fixable-but-annoying paperwork later.

### Business licenses

Depending on what you do and where, you may need:

- **State-level license** (most common: professional services,
  contracting, retail). Check your state's Department of Business or
  equivalent.
- **City-level business license** (most US cities require one for
  any business operating within city limits, including home offices).
  Typically $50–$300/yr.
- **County-level filings** (some counties — varies).
- **Industry-specific licensure:** if you sell food, alcohol,
  firearms, financial products, healthcare services, legal services,
  etc., expect additional licensing.

The fastest way to figure out what applies: search "{{state}} business
license requirements {{your industry}}" and call your city's small-
business office. They'll tell you what you need in 10 minutes; saves
hours of guessing.

---

## Operating agreement (LLCs) / bylaws (corps) / partnership agreement (LLPs)

Even if your state doesn't legally require one, write one. The
document that says "who owns what, who decides what, what happens if
someone leaves or dies" is the load-bearing artifact when something
goes wrong. Don't skip this.

For single-member LLCs, the agreement is short (~3 pages) and mostly
formalizes the founder's structure. For multi-member entities, this
is the most important legal document the company has — pay an
attorney $500–$2,000 to draft or review, depending on complexity.

The seed deliberately does NOT ship a template operating-agreement /
bylaws / partnership-agreement at v0 — these vary too much by state
and by company structure to template safely. Common starting points:

- **LLC operating agreement:** state bar associations often publish
  free templates; LegalZoom and Rocket Lawyer have paid templates;
  Cooley GO has free templates aimed at startups (corp-shaped, but
  the LLC variants are decent).
- **C-corp bylaws + stockholders agreement:** Cooley GO, Y Combinator's
  SAFE templates (for the financing instrument), Orrick's Total Access
  documents.
- **LLP partnership agreement:** ask your state bar's
  practitioner-resources page; this is the area where boilerplate
  most often fails and where counsel is cheapest as insurance.

---

## What the seed does NOT ship

- State-specific regulatory packages (broker-dealer registration,
  HIPAA Business Associate Agreements, food-service licensing). Industry-
  specific.
- 409A valuations or cap-table software (use Carta / Pulley when
  needed).
- Trademark / IP filings — use an attorney or LegalZoom-class service.
- Visa / immigration paperwork for foreign founders or employees.
- Operating agreements / bylaws / partnership agreements (see above).

---

## Graduation path — when this layer outgrows one README

When this README has grown past ~500 lines, or when you have multiple
contract templates piling up at the bottom, split into:

```
10-legal/
├── README.md                       # this file, leaner
├── shape-llc.md                    # LLC formation walkthrough
├── shape-corp.md                   # C-corp formation walkthrough
├── shape-llp.md                    # LLP formation walkthrough
├── shape-sole-prop.md              # sole-prop / DBA walkthrough
├── ein-walkthrough.md              # detailed EIN steps
├── registered-agent.md             # comparison table
├── business-license.md             # state + city + county checklist
└── templates/                      # contract templates
    ├── nda-mutual.md
    ├── nda-one-way.md
    ├── contractor-agreement.md
    ├── employment-offer.md
    ├── ip-assignment.md
    └── operating-agreement.md
```

Don't pre-build any of this. Add as you earn it.
