# Atomic-Lab Lifecycle

## States

A lab is always in exactly one lifecycle state. Transitions are
recorded in events.log.

```
      born                     parked                     graduated
        │                        │  ┌─────────────────────────►
        ▼                        │  │
     ┌──────┐  thread_opened   ┌─────────┐               ┌───────────┐
     │ idle │ ───────────────► │ working │ ────────────► │ completed │
     └──────┘                  └─────────┘               └───────────┘
        ▲                        │  │
        │                        │  └────────────────────►  abandoned
        │                        │                         ┌───────────┐
        └────── thread_closed ───┘                         │           │
                                                           └───────────┘
```

## Birth

`event=lab_born`

The very first event in events.log. Marks the moment CHARTER.md +
IDENTITY.md + STATE.md exist on disk and the lab is operational.

After birth: `state=idle`. No threads open yet.

## Working

A lab is `working` when at least one thread is `open` (not `parked`,
not `closed`, not `graduated`).

Sub-state for each thread:
- `open` — actively being investigated
- `parked` — blocked on an external (token, decision, dependency,
  upstream change). Lab continues to live; thread waits.
- `graduated` — answered, moved off the open list. Findings remain.
- `closed` — abandoned, no longer relevant.

Transitions:
- `event=thread_opened name=X` — opens a thread
- `event=thread_parked name=X reason=Y`
- `event=thread_graduated name=X answer_via=Z`
- `event=thread_closed name=X`

## Experiment lifecycle

Within a thread, experiments run:

- `event=experiment_started exp=X`
- `event=experiment_concluded exp=X verdict=kept|reverted|inconclusive`

Verdicts:
- `kept` — hypothesis confirmed; the experiment's output is reusable
- `reverted` — hypothesis disconfirmed OR the experiment surfaced a
  bug; back to drawing board
- `inconclusive` — experiment ran but didn't answer the question
  (often blocked); produces a finding even though the original
  question is still open

## Sub-lab spawning

`event=sublab_spawned name=X`

Parent lab spawns a sub-lab when a thread surfaces a domain that
warrants its own ongoing capability. Sub-lab is a full atomic-lab
(eight dirs, three top-level docs, its own events.log). Parent
references via STATE.md.

## Director communication

- `event=decision_request_emitted id=NNN topic=X` — lab put a
  decision-request in outbox/
- `event=director_decision payload=X` — director's reply landed in
  inbox/
- `event=report_emitted name=X` — lab pushed a finding/confirmation to
  outbox/
- `event=report_received from=Y name=X headline=Z` — typically a
  sub-lab reporting up to its parent

## Promotion

When a lab produces something reusable beyond itself:

- `event=artifact_promoted name=X status=candidate|graduated`
- `event=playbook_captured name=X scope=lab|parent_lab`

`candidate` lives in `artifacts/candidates/`. `graduated` has been
moved to a higher-level home (a runbook, a CLI subcommand, a tooling
primitive).

## Completion

A lab can be `completed` when:
- All threads are graduated or closed
- No outstanding outbox items
- STATE.md headline reads "complete"
- events.log records `event=lab_completed`

Completed labs stay on disk as a reference. They're not deleted.

## Abandonment

A lab can be `abandoned` if its premise is invalidated. STATE.md
records why; events.log gets `event=lab_abandoned reason=X`. The lab
stays on disk; its threads close; nothing else changes.

## Re-opening

A completed or abandoned lab can be re-opened if circumstances change.
A new charter amendment supersedes the old one; events.log records
`event=lab_reopened reason=X`.

## State transitions (canonical)

| From | To | Event |
|---|---|---|
| (nonexistent) | idle | `lab_born` |
| idle | working | `thread_opened` (the first one) |
| working | working | `thread_opened`, `experiment_started`, etc. |
| working | idle | last open thread parks, graduates, or closes |
| working | completed | last open thread graduates AND charter satisfied |
| working | abandoned | premise invalidated |
| any | idle | `lab_reopened` (after completed/abandoned) |
