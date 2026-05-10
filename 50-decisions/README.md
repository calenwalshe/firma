---
layer: decisions
status: template
---

# Decisions — How this company decides

The decision layer answers: who calls what, when, how is it recorded,
and how does someone reading this in 18 months know why?

---

## Decision rights

Pick one shape (edit; delete the others):

### Single-decider

- **Best for:** sole-founder shapes; small teams where one person owns
  the company-shape calls.
- **Rule:** the founder calls every shape-changing decision. ADRs in
  `decisions/` are the record.

### Two-or-three-co-founders

- **Best for:** partnerships, founding teams of 2–3.
- **Rule:** consensus on shape-changing decisions; one named lead
  breaks ties. ADRs record the decision; if there's dissent, the ADR
  records the dissenting view (per Principle 8 in
  `00-foundation/PRINCIPLES.md`).

### Voting (with quorum)

- **Best for:** larger founding teams, professional partnerships
  (LLPs especially), companies with formal board governance.
- **Rule:** majority vote on shape-changing decisions; quorum named
  in operating agreement / partnership agreement / bylaws. ADRs
  record the count.

### Board-led (corp shape)

- **Best for:** companies with outside investors and a formal board.
- **Rule:** board votes on company-shape calls; CEO calls operational
  matters within board-set guardrails. ADRs are the operational
  record; board minutes are the formal record.

---

## What gets an ADR

An ADR (Architecture Decision Record — applied broadly) is required
when the decision **changes the shape of the company**:

- Legal-entity changes (incorporating, foreign-qualifying, dissolving,
  changing tax election).
- Brand-stance changes (founder appears publicly / no longer does;
  rename; trademark filing).
- Customer-segment changes.
- Pricing model changes.
- Inheritance-posture changes (e.g. starting to use the kernel; moving
  off it).
- Sunset condition changes.
- Hires that change governance (first W-2 employee; first executive;
  first board member).
- Material vendor / banking / infrastructure changes (changing banks,
  changing accounting software at scale, changing hosting providers
  at scale).

What does NOT get an ADR:

- Day-to-day operational choices (those go in a labbook or daily-
  notes pattern, not the decision log).
- Code-level decisions (those go in code review or `KNOWN_ISSUES`
  files in your engineering layer).
- Things you can freely undo without external impact.

---

## ADR shape

See [`ADR-TEMPLATE.md`](ADR-TEMPLATE.md). Every ADR has these
sections:

- **Context.** What's the situation that requires a call?
- **Decision.** The call, in 1-2 plain-language sentences.
- **Consequences.** What changes — both upside and new constraints.
- **Alternatives considered.** What else was on the table; why each
  was rejected.
- **Cross-references.** Other ADRs (parent, related), kernel labs
  if any, external docs.

ADRs are append-only. You don't edit a past ADR. If a past decision
needs revisiting, write a new ADR that supersedes the old one and
say so explicitly in the new ADR's Context.

---

## RACI (when you have a team)

For each significant ongoing function or recurring decision, name who
is **R**esponsible (does the work), **A**ccountable (signs off — the
single named person), **C**onsulted (input before the decision),
and **I**nformed (told after).

At <5 people: skip the formal RACI. Decisions are obvious.

At 5–10 people: write a one-page RACI for the recurring decisions
that crop up (hiring, pricing changes, vendor selection, customer-
escalation handling). Lives in `50-decisions/RACI.md` when you build
it.

---

## Board governance (corp shape only)

If you're a C-corp or LLC-with-board:

- **Quorum:** named in bylaws / operating agreement.
- **Cadence:** quarterly minimum; monthly is common at early stage.
- **Minutes:** kept formally (not in this layer; they live in
  `90-operations/compliance/board-minutes/` when you build it).
- **Resolutions:** specific board-approved actions get a written
  resolution. Vendor (Carta, Pulley, Ironclad, or attorney-drafted)
  generates these.

If you don't have outside investors, your "board" is functionally
the founders. You still need to follow corporate formalities (annual
meeting, recorded minutes) to maintain the corporate veil. Don't skip.

---

## Graduation path

When this layer outgrows one file + ADR template:

```
50-decisions/
├── README.md
├── ADR-TEMPLATE.md
├── RACI.md                    # who-decides-what for recurring choices
└── BOARD-GOVERNANCE.md        # for corp shape with formal board
```

The `decisions/` directory at the repo root is the actual ADR log
(separate from this layer's templates).
