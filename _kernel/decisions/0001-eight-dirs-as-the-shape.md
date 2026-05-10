# ADR 0001 — The eight-dir shape is the contract

**Status:** accepted
**Date:** 2026-05-02

## Context

The first atomic-lab settled on a specific directory layout: three
top-level `.md` files (CHARTER, IDENTITY, STATE) plus one append-only
file (events.log) plus eight directories (inbox, outbox, threads,
experiments, sublabs, memory, journal, artifacts).

The question: is this layout *the contract* (every atomic-lab MUST
have it) or *a convention* (suggested but not required)?

## Decision

**The eight-dir shape is the contract.** Every atomic-lab MUST have
the same eight directories and the same three top-level files, even
when some are empty. Predictability is the point.

## Rationale

- A director scanning a new atomic-lab knows exactly where to look for
  current state (STATE.md), pending decisions (outbox/), open work
  (threads/), runs (experiments/), and history (events.log). No
  variance in layout means no exploration overhead.
- Tooling that operates on atomic-labs (cross-lab dashboards, summary
  scripts, future scaffolding CLIs) can rely on the layout existing.
- Empty-but-present dirs cost nothing on disk and signal "this kind of
  work is supported but hasn't happened yet."
- A lab that omits a dir is harder to extend later than one that has
  it empty — the empty dir is an invitation.

## Consequences

- The template at `template/` ships with all eight dirs (each
  containing a `.gitkeep`).
- A new lab MUST scaffold the full shape, not a subset.
- A lab missing a dir is a bug to fix, not a stylistic variation.
- Adding a *ninth* directory requires its own ADR (this ADR amended
  or superseded). Do not silently extend the shape.

## Alternatives considered

- **Optional dirs.** Rejected — variance in layout breaks the
  scannability promise. The cost of an empty dir is zero; the cost of
  uncertainty is real.
- **Different shapes per lab kind.** Rejected — atomic-lab is the lab
  kind; further specialization happens via charter content, not
  structural difference.
- **Flatter layout (no `experiments/threads/sublabs/` separation).**
  Rejected — these three are conceptually distinct (one-shot vs
  long-running vs nested) and conflating them makes verdicts
  ambiguous.

## Followups

When the system gains new first-class concepts (e.g. a `tick-history/`
dir for an automated runtime), they get their own ADRs. The shape is
amendable but not silently.
