# Atomic-Lab Protocol Roadmap

Where this is going. Each milestone is a research target, not a ship
date. Versions are loose; convention stability matters more than
release cadence.

> **Why "experimental" is the loud word.** This roadmap is honest
> about what hasn't happened yet. v0.1 is one operator, one machine,
> a few weeks. Anything past v0.2 is provisional.

---

## v0.1 (current) — extracted, single-operator-tested

- ✅ Eight-dir shape
- ✅ CHARTER / IDENTITY / STATE / events.log discipline
- ✅ inbox/outbox protocol with decision-request format
- ✅ Bounded experiments with verdict.json
- ✅ Recursive sub-labs
- ✅ ADRs 0001/0002/0003 ported and generalized
- ✅ `bin/labbook-commit` with pluggable synth (default: no LLM)
- ✅ `template/` + `docs/getting-started.md`

What v0.1 ships: an inhabited workspace shape that has held up
under one operator's real work. The pattern is documented; the
helper runs against any directory that's a git repo.

What v0.1 does NOT ship: any guarantee that the conventions are
right for anyone but the original operator.

---

## v0.2 — dogfooded in a second project

The big test. The protocol survives — or doesn't — when applied to a
domain it wasn't extracted from.

- [ ] Pick one external project (a research project, a creative
      project, an engineering effort, whatever) and run a real
      atomic-lab inside it for 2-4 weeks
- [ ] Capture friction in a `notes-from-dogfood.md`
- [ ] Either: ship the friction-driven changes as v0.2, or document
      that the protocol is over-fit and pull v0.1 back to "draft"

What v0.2 will probably surface:
- Event names that mean different things in different domains
- Charter sections that don't apply to certain kinds of work
- Labbook-commit synthesis quality with the default (no-LLM) mode

Open questions for v0.2:
- Is the `<wrapper>/labs/` layout actually what people want, or
  should each lab be its own repo?
- Does "director" carry the right connotations outside an
  agent-harness context?
- Is the 15-event vocabulary the right size, or should it shrink to
  ~7?

---

## v0.3 — convention-stable; first user-friendly version

Once dogfooding has surfaced enough friction to know what's wrong:

- [ ] Stabilize the event vocabulary (lock-in or breaking-change
      release)
- [ ] Stabilize the eight-dir names
- [ ] Improve `bin/labbook-commit` based on actual usage (better
      default synthesis, optional LLM hooks documented)
- [ ] Add 1-2 worked examples in `examples/`
- [ ] Document an upgrade path from v0.x labs to v0.3 labs

This is the version a curious person could clone and try without
expecting things to break.

---

## v1.0 — stability commitment

Date: TBD. Comes when the protocol has survived dogfooding by more
than one operator and the conventions have been stable for at least
3 months.

After v1.0:
- Breaking changes require a major version bump and a written
  migration path
- Event vocabulary is frozen at the system layer
- The eight-dir shape is the contract for the foreseeable future

---

## Open research questions

These shape future versions but don't fit a specific milestone:

1. **Lifecycle of a "completed" lab.** Stays on disk forever, or
   archives after N months of inactivity?
2. **Memory consolidation.** When `memory/playbooks/` grows past N
   entries, does the lab need a librarian to organize them?
3. **Sub-lab graduation.** When does a sub-lab become a sibling lab
   instead?
4. **Cross-lab promotion.** A pattern lifts from one atomic-lab to a
   shared dir. What's the ceremony?
5. **Multi-director.** Whole pattern assumes one director. What does
   a multi-director mode look like?
6. **An async runtime.** A lab running between director sessions —
   tick loop, coordinator, parallel threads — is sketched in
   ARCHITECTURE but not built. v1+ territory.

These are tracked here so they don't get lost. ADRs land in
`decisions/` when answered.
