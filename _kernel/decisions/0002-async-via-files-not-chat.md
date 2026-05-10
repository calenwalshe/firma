# ADR 0002 — Director ↔ lab via files, not chat

**Status:** accepted
**Date:** 2026-05-02

## Context

In many agent harnesses, an operator and a working agent communicate
through a synchronous chat — the agent types, operator reads, operator
types back, agent reads. Conversation drifts in the agent's session
log. Once the session ends, the dialog scrolls away.

An atomic-lab needs a different protocol because:

- Many atomic-labs are designed to operate **between director
  sessions** (a future tick loop). A synchronous chat doesn't survive
  when the director isn't attached.
- The director may want to **scan multiple labs' status without
  attaching** to any of them. Chat-based status requires an attach.
- Some decisions need a **durable, structured shape** (options,
  recommendation, what-happens-after). Chat is too freeform.
- The director may want to **respond when ready**, not when the lab
  pings.

## Decision

Director ↔ lab communication for atomic-labs happens via files in
`inbox/` (director → lab) and `outbox/` (lab → director). Both are
flat directories of `.md` files following the conventions in
`PROTOCOL.md`.

The lab and director never use a synchronous chat surface to negotiate
across the boundary. The agent's chat is for the lab's *internal*
work; cross-boundary asks always go through files.

## Consequences

- The lab MUST emit a `decision_request_emitted` event when it writes
  a structured ask. This makes async work observable.
- The director can scan all labs' outboxes in one pass to triage.
- The decision-request format (situation, options, recommendation, what
  I'll do after) is enforced — labs that emit empty asks are violating
  the protocol, not just being lazy.
- The protocol survives any future async-runtime transition: a tick
  loop just means outbox items pile up between visits.

## Why files, specifically

Considered alternatives:

- **A queue daemon (e.g. Redis).** Rejected — adds infrastructure
  dependency for a single-director, single-machine system. Files are
  zero-dep and human-readable.
- **A SQLite db per lab.** Rejected — same dep argument; also losing
  human-readability of the messages themselves.
- **Persistent chat in a terminal pane.** Rejected — chat scrolls;
  files don't. Chat doesn't structure; files do.
- **A web UI dashboard.** Out of scope for v0.1; might layer ON TOP of
  the file protocol later, but the protocol stays file-based
  underneath.

## Cost

- Director must remember to actually read the outbox. A future status
  CLI can surface staleness; until then, manual.
- Lab can emit too many outbox items. Mitigation: charter caps
  decision-requests per session (default: 3) and the lab batches.

## What this enables

- An async runtime where labs can keep working between director
  sessions, because the protocol doesn't require synchrony.
- Cross-lab decision relay — sibling labs could read each other's
  outboxes (a future extension, same shapes).
- Audit — every director decision is permanently in `inbox/`, every
  lab ask is permanently in `outbox/`. Replay is trivial.
