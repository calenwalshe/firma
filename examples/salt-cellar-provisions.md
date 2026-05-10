# Worked example — Salt-Cellar Provisions (synthetic)

This file is a **synthetic worked example** — what the scaffold looks
like with placeholders filled in. The workspace named here
("Salt-Cellar Provisions") is fictional, chosen to be specific enough
that the example reads like a real one but distant enough from any
real operation that no one mistakes it for an active business.

This particular example is shaped as a small commerce operation — one
pattern. The same scaffold instantiates differently for a research
project, a service practice, a side build, or any other complex
workspace; the layer set adapts to what the workspace actually needs.

The example fills in CHARTER.md and the founding ADR end-to-end, then
walks through what got filled in — and what got deferred — across
each of the nine layers on setup day.

---

## The shape

**Salt-Cellar Provisions** is a one-person artisanal salt e-commerce
business in coastal Maine, founded by Hannah Reeve (fictional). She
hand-harvests sea salt from Penobscot Bay, ages it with smoked
applewood and spruce tips, and sells flake and finishing salt direct
to consumers (DTC via website) and wholesale to specialty grocers in
the Northeast US.

She founded it on 2026-05-01 as a Maine sole-proprietorship, with a
plan to convert to a single-member LLC at the end of year 1 if
revenue clears $25,000.

---

## CHARTER.md (filled)

```markdown
---
layer: foundation
status: stable
last_reviewed: 2026-05-01
review_cadence: quarterly
---

# Salt-Cellar Provisions — Charter

## Definition

Salt-Cellar Provisions is a one-person artisanal salt operation
producing hand-harvested sea salt from Penobscot Bay, Maine.

It is a sole-proprietorship, formed in Maine on 2026-05-01.

## Why it exists

The Northeast US has a small but committed market for finishing
salts — restaurants, specialty grocers, and home cooks — that is
mostly served by imports (Maldon, Halen Môn, Jacobsen). No
established Maine producer makes a flake-style finishing salt at
craft scale, despite the state having one of the longest cold-water
coastlines in the contiguous US. The work to claim that gap has a
clear shape: harvest, refine, package, sell.

This is the right venture for one operator with a coastal property,
food-safe processing space, an existing relationship with the
Maine Department of Agriculture's small-producer program, and a
12-month commitment to focus on this specific market. It is not the
right venture for a multi-person team or for a wholesale-first
operation; both shapes would dilute the boutique positioning that
the brand depends on.

## What it is

1. **Concretely.** A maker-operated artisanal salt producer; flake
   sea salt, smoked salt, and one or two seasonal/specialty salts.
2. **Structurally.** A Maine sole-proprietorship at v0; planned LLC
   conversion at year-end if revenue clears $25,000.
3. **Strategically.** A boutique brand competing on terroir
   (Penobscot Bay specifically) and on a small, deeply-considered
   product line, not on volume or low cost.

## What it is not

1. Not a wholesale salt distributor. (Salt-Cellar sells direct to
   end customers and to a small set of specialty grocers; volume
   wholesale to large chains is out of scope at v0.)
2. Not a bulk industrial-grade salt producer. (Industrial flake
   salt margins are too thin; the brand competes on craft, not
   cost.)
3. Not a multi-product gourmet line. (No sugar, no spices, no
   condiments — sticking to salt as the focal product. Adding
   adjacent product lines is a year-2-or-later decision.)

## Who it serves

- **Independent specialty grocers** in Maine, New Hampshire,
  Massachusetts, Rhode Island, and Vermont — typically 2-10 store
  chains buying a case of jars at a time.
- **Direct-to-consumer home cooks** ordering 1-3 jars at a time
  from the website.
- **Restaurant chefs** in the same five-state region, sourcing
  finishing salt for plate-up and seasonal menus.

## Brand stance

Public-facing under the Salt-Cellar Provisions brand. Hannah Reeve
appears under her own name where the field calls for it (founder
photo on the about page, founder-led customer email replies for
wholesale inquiries, founder-quoted in any local press coverage).
This is a maker-led brand; founder anonymity would be wrong shape.

## Sunset

Disprove-bound. Salt-Cellar Provisions closes on 2027-05-01 unless:

- [ ] First $5,000 in DTC + wholesale revenue, AND
- [ ] At least three repeat wholesale accounts, AND
- [ ] Quarterly cost-of-goods is below 60% (gross margin >40%).

If at least two of three are tracking, the company continues. If
only one is tracking, the founder writes a refresh-CHARTER ADR with
revised disprove conditions and a new clock. If zero are tracking,
the company winds down per the protocol in `BOOTSTRAP.md`.

## Constraints (always live)

1. **Maine cottage food / small-producer compliance** — every
   product produced under Maine Department of Agriculture's small-
   producer registration; nothing sold off-site without proper
   labeling.
2. **No co-packing at v0** — the brand is "made by hand at one
   coastal Maine location." If demand exceeds capacity, the founder
   chooses between (a) raising prices, (b) limiting allocation, or
   (c) explicitly recording an ADR before any co-packing arrangement.
3. **No drop-shipping, no Amazon at v0** — DTC is via the company's
   own website only. Maintains brand and customer relationship
   directly.
4. **No outside investment in year 1** — the disprove date and
   conversion to LLC come first. Investment conversation is a
   year-2 question if at all.
5. **Quarterly book close** — books are reconciled in Wave by the
   end of the second week after each quarter.
```

---

## The founding ADR (filled)

```markdown
---
id: 0001
date: 2026-05-01
status: decided
parent_adr_refs: []
---

# ADR 0001 — Founding Salt-Cellar Provisions

## Context

Hannah Reeve has a coastal property in Penobscot Bay, Maine, with
food-safe processing space and an existing relationship with the
Maine Department of Agriculture's small-producer program. She has
spent six months hand-harvesting and aging salt as a hobby, and
three local grocers have asked when they can carry it commercially.
The work has reached the point where it should either become a
real venture or be set aside. This ADR captures the founding
decisions.

## Decision

Found Salt-Cellar Provisions as a Maine sole-proprietorship on
2026-05-01, with the following parameters:

- **Legal shape:** Sole-proprietorship at v0; planned LLC conversion
  on or before 2027-05-01 if revenue clears $25,000.
- **State of formation:** Maine.
- **Registered agent:** N/A (sole-prop; founder is the surface).
- **Founders / owners:** Hannah Reeve, sole owner.
- **Brand stance:** Public-facing under Salt-Cellar Provisions
  brand; founder appears under her own name in maker-led contexts.
- **Domain:** saltcellarprovisions.com (registered 2026-04-28 via
  Cloudflare Registrar, $9.39/yr).
- **Sunset condition:** Disprove-bound; see CHARTER §Sunset for
  the three-condition test on 2027-05-01.

## Consequences

- The company exists as a sole-proprietorship; income flows to
  Hannah Reeve's personal Schedule C; no liability shield until
  LLC conversion.
- Maine state business registration filed 2026-05-01; small-producer
  food registration filed concurrently.
- Federal EIN obtained 2026-05-02 (~15 minutes online).
- Banking: Bangor Savings Bank business checking, opened 2026-05-04
  (in-person; preferred over Mercury for the cash deposits Hannah
  takes at farmers markets).
- Books: Wave (free) at v0; QuickBooks consideration deferred to
  LLC conversion.
- The founder owns all IP and product formulas (no contractors yet
  to require IP-assignment).
- Insurance: General Liability through Hiscox, $850/yr, bound
  2026-05-06 (before first wholesale shipment).
- Maine sales tax permit obtained 2026-05-08 (required for any
  retail sales in Maine).

## Alternatives considered

- **Form an LLC immediately.** Rejected. The first year is genuinely
  exploratory — disprove-bound. If the business doesn't clear
  $25,000 revenue in year 1, the LLC formation cost ($175 Maine LLC
  filing + ~$85 annual fee + Northwest registered agent ~$125/yr)
  is not recovered. Sole-prop at v0 is reversible (convert to LLC
  later); LLC at v0 is harder to back out of.
- **Form a Wyoming LLC for privacy/cost.** Rejected. The business
  operates in Maine; foreign-qualifying in Maine on top of a Wyoming
  LLC adds cost and complexity for no benefit. Maine sole-prop now,
  Maine LLC later, is the cleaner path.
- **Operate as a hobby and sell informally.** Rejected. Three
  grocers have asked to carry the product commercially; there's an
  obvious legal-shape upgrade required (Maine small-producer food
  registration, sales-tax permit, GL insurance) that pushes the
  work past hobby scale. Doing those steps without forming a
  business is needless paperwork friction.

## Why this over alternatives

The disprove date forces a real test of demand within 12 months.
Sole-prop minimizes upfront cost and maximizes optionality —
upgrade-to-LLC if disproven; wind down with no entity dissolution
if it doesn't work out. Maine over Wyoming because the business
is physically tied to Maine and there's no liability or tax case
for a Wyoming entity here.

## Cross-references

- CHARTER: `00-foundation/CHARTER.md`
- Legal posture details: `10-legal/README.md`
- Bank choice: `20-financial/README.md`
```

---

## Layer-by-layer instantiation (day 0)

### 00-foundation
- **CHARTER.md** — filled (above).
- **PRINCIPLES.md** — filled with 5 principles. Hannah kept #1 (Do
  the obvious thing first), #3 (Customers are not adversaries), #4
  (Money runs the calendar), #7 (The website is a contract), and
  added one: "Salt is the product. Anything else is for after the
  salt is right."

### 10-legal
- **README.md** — left as-is from the seed; the four-shape
  walkthrough is reference material, not custom-edited per
  instantiation.
- **Real legal artifacts** kept off the repo: Maine small-producer
  registration, sales-tax permit, GL insurance certificate. Lives
  in a `legal/` subdirectory in Hannah's local Dropbox, not committed
  to the public repo.

### 20-financial
- **README.md** — left as-is, with one customization: noted "Bangor
  Savings, not Mercury, because cash deposits at farmers markets"
  in a paragraph at the top.
- **Bank account** opened (Bangor Savings).
- **Books** in Wave, set up 2026-05-04.
- **Runway model** — no formal CSV at v0; Hannah has a one-page
  Numbers spreadsheet (kept off-repo) tracking expected jar count
  per month vs cost-of-goods. To be promoted to the layer when it
  graduates.

### 30-brand
- **README.md** — customized with: name story (Salt-Cellar = a
  small, sturdy table cellar for finishing salt; Provisions =
  pantry-shape, not gourmet-shape); Penobscot Blue (#3a5a7c) as
  accent over the warm-black/off-white default; Playfair Display
  for the wordmark; Inter for body. SVG logo (a stylized cellar)
  deferred to month 2.
- **USPTO TESS:** searched 2026-04-25; "Salt Cellar Provisions"
  clear in Class 30 (food). Filing deferred.

### 40-comms
- **README.md** — customized: removed the section on internal team
  comms (one-person company), kept external + customer.
- **Website:** single-page static HTML at saltcellarprovisions.com,
  hosted on Cloudflare Pages. Three sections: hero, products,
  contact. Built in 6 hours over one weekend.
- **Email:** hannah@saltcellarprovisions.com via Google Workspace,
  $7/month.
- **Help alias:** help@saltcellarprovisions.com forwards to
  hannah@.
- **Social:** Instagram (@saltcellarprovisions, claimed). LinkedIn
  not claimed; not a B2B-shaped venture.

### 50-decisions
- **README.md** — left as-is; single-decider posture.
- **ADR-TEMPLATE.md** — left as-is.
- **Founding ADR** signed and committed (above).

### 60-team
- **DELETED.** Hannah is solo by design at v0; the seed's
  recommendation when this is the case is to delete the layer. The
  founding ADR records "single-operator-by-design" so a future
  reader knows it was a deliberate cut.

### 70-sales
- **README.md** — customized. Markdown CRM in `customers/`. Three
  stub files at v0:
  - `customers/_example.md` (the shape)
  - `customers/the-corner-store.md` (Portland ME; verbal commitment
    to carry; awaiting wholesale sample)
  - `customers/seacoast-grocer.md` (Portsmouth NH; introduced
    via referral; first conversation 2026-04-22)
- **Billing:** Stripe for online DTC; Square for farmers-market
  card payments; invoicing for wholesale via Wave.

### 80-product
- **DELETED at v0.** Hannah's "product" is the salt itself; product
  development is craft, not software-shaped specs and roadmaps. If
  Salt-Cellar adds a digital surface (recipe app, salt-of-the-month
  subscription product), 80-product/ comes back. Founding ADR
  records the cut.

### 90-operations
- **README.md** — customized with the actual vendor register at v0:
  Cloudflare ($0/mo for DNS, ~$10/yr for domain), Google Workspace
  ($7/mo), Wave ($0/mo), Hiscox GL ($850/yr), Stripe (per-transaction),
  Square (per-transaction), Bangor Savings ($0/mo).
- **Insurance:** GL bound (above).
- **Compliance:** Maine small-producer food registration on file;
  Maine sales-tax permit on file; both linked from a `compliance/`
  subdirectory in Hannah's local Dropbox (not committed).
- **Privacy policy / terms:** generated via iubenda for the website,
  $30/yr.

### _kernel
- **Submoduled.** Hannah hasn't spawned a lab yet; the kernel sits
  unused at v0. Plan: when she's deciding whether to add a salt-of-
  the-month subscription product (probably ~month 6), spawn a lab
  to investigate pricing and demand.

### decisions
- **0001-founding.md** — signed (above).

---

## What month 1 looked like

End of month 1 (2026-05-31):

- 6 jars sold DTC ($168 revenue at $28/jar).
- 1 wholesale order shipped (The Corner Store, $186 wholesale).
- Total revenue: $354.
- Total cost-of-goods: $89 (jars + labels + shipping).
- Total expenses: $354 (formation $50 + GL $850 prorated + Workspace
  $7 + bank $0 + Wave $0 + Stripe fees $5).
- Net month: -$0 cash-flow ($354 in, $354 out — but $850 of the
  expense is the GL annual premium, so actual recurring monthly
  burn is much lower).

The disprove date is 2027-05-01. Hannah is on track if she clears
~$420/month in revenue by Q4 of year 1. At month 1, she's at $354;
the trajectory is on the line but not yet conclusive. Quarter 1
review will be the first real check.

---

## What this example demonstrates

1. **Layer-deletion is a real pattern.** Salt-Cellar deleted
   `60-team/` and `80-product/` at v0. Most companies will delete
   2–3 layers at founding; that's the seed working as designed, not
   a missing-feature.

2. **Sole-prop is a valid v0.** The seed's defaults nudge toward
   LLC, but the worked example shows a sole-prop is a reasonable
   shape when the founder genuinely wants reversibility and low
   upfront cost.

3. **The disprove date works as a forcing function.** Without it,
   Salt-Cellar could limp along for 3 years at $300/mo. With it,
   2027-05-01 forces a real conversation: is this working?

4. **The seed handles non-tech-shaped businesses.** Salt-Cellar is
   not SaaS, not consulting, not online-first. It's a coastal Maine
   food-craft business. The seed's templates worked anyway because
   the underlying questions — what is this, who is it for, who
   decides, where does the money go — are universal.

5. **Most of the artifacts are off-repo.** Customer files, financial
   data, formal legal documents stay out of the public/private
   business repo (per `.gitignore`). The repo carries the *shape*,
   not the *substance*.

A real instantiation should look about this length when filled —
~500 lines of CHARTER + ADR + lightly-customized layer READMEs — not
4,000 lines, not 80 lines.
