# Atomic-Lab Protocol — inbox / outbox

How a lab and its director communicate via files. Async, durable,
reviewable.

---

## Why files (not chat)

Atomic-labs communicate via files because:

- **Durability.** A file persists across sessions; chat scrolls away.
- **Reviewability.** The director can read every outbox item without
  attaching to the lab's session.
- **Asynchrony.** The director responds when ready; the lab waits
  without burning context.
- **Typed structure.** Files have headers, sections, formats — chats
  drift.
- **Multi-lab attention.** The director can scan all labs' outboxes in
  one pass.

If your operator surface (whatever drives the lab) supports
synchronous chat, that surface is for the lab's *internal* work.
Cross-boundary asks always go through files.

---

## Outbox — lab to director

The lab writes a `.md` file to `outbox/`. Naming convention encodes
the kind:

| Pattern | Meaning |
|---|---|
| `decision-request-NNN-<topic>.md` | Structured ask with options. Director MUST respond. |
| `<kind>-report-NNN-<topic>.md` | Finding the lab wants visible. Director MAY respond. |
| `<kind>-confirmation-<topic>.md` | Confirmation of a completed action. Informational. |

`NNN` is a 3-digit zero-padded counter, monotonic per lab.

### Decision-request format

Every decision-request has the same shape:

```markdown
# Decision request NNN — <short title>

**From:** <lab-name>
**To:** director
**Date:** YYYY-MM-DD
**Blocking:** thread `<thread-name>` (or null)

## Situation
What's the lab's current state? What surfaced this need?

## Options

### A. <short label>
Description. Cost. Risk. Lifetime.

### B. <short label>
…

### C. <short label>
…

## My recommendation
Which option, and why.

## What I'll do once <X>
Concrete next steps after the director responds.
```

The lab MUST emit `event=decision_request_emitted id=NNN topic=X` to
events.log when it writes the file.

### Report format

Less rigid. Headline + structured body. Examples:

- `delivery-state-report-001-from-browser-sublab.md` — sub-lab tells
  parent "I checked the upstream state, here's what I saw"
- `pause-confirmation-and-promotions.md` — lab confirms it paused the
  pipeline and promoted two playbooks

### Discipline

- One outbox file per concern. Don't pile multiple decisions into one
  file.
- Filename describes the topic clearly.
- Once the director answers (in inbox/), the outbox file STAYS — it's
  the durable history.

---

## Inbox — director to lab

The director writes a `.md` file to `inbox/`. The lab reads it next
session and acts on it.

| Pattern | Meaning |
|---|---|
| `response-NNN-<topic>.md` | Reply to outbox/decision-request-NNN. |
| `directive-<topic>.md` | Unsolicited instruction. |

### Response format

Conventional but not strict:

```markdown
# Response NNN — <short>

**To:** <lab-name>
**From:** director
**Date:** YYYY-MM-DD
**Re:** outbox/decision-request-NNN-<topic>.md

## Decision
A short answer (e.g. "B") followed by reasoning.

## Constraints / addenda
Any extra context the lab needs.
```

### Directive format

Unstructured. Often a single paragraph. The lab interprets and acts.

### Discipline

- Once the lab acts on an inbox item, it remains on disk as history.
- The lab MUST emit `event=director_decision payload=<short>` when it
  consumes a response or directive.

---

## State during the protocol

When a lab is waiting on the director:

- The corresponding thread is `parked` (with `reason=awaiting_director`)
- STATE.md notes "Waiting on director for X"
- The lab does not start new work that depends on the answer
- It MAY work on unrelated threads

When the director's response lands:

- Lab unparks the thread
- Updates STATE.md headline
- Resumes work
- Logs `director_decision`

---

## Anti-patterns

- **Empty decision-requests.** "What should I do?" without options is
  not a decision-request; it's the lab dodging work. The lab must
  produce 2-4 viable options before asking.
- **Mega-files.** Don't put 12 decisions in one outbox file. One
  decision per file.
- **Implicit waiting.** A lab that starts a long-running task and then
  stops without an outbox item leaves the director confused. Always
  emit `decision_request` or `report` when state changes externally.
- **Inbox without acknowledgment.** A lab that receives an inbox
  response but doesn't update events.log makes the history opaque.

---

## Forward compatibility

The file shapes here are designed to survive future versions:
- A tick loop (lab runs between director sessions): outbox items pile
  up; director reviews on next visit. Same shapes.
- A web dashboard reading outbox/: layers on top, doesn't replace.
- Cross-lab decision relay (sibling labs reading each other's
  outboxes): same naming conventions; only the consumer changes.

The protocol is forward-compatible by design.
