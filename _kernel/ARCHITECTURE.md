# Atomic-Lab Architecture

The full description of what an atomic-lab is, what it contains, and how
its parts fit together.

---

## Core definition

> An atomic-lab is an **inhabited workspace** for a single coherent
> long-running concern, with explicit charter, identity, state, async
> file-based director communication, bounded experiments, recursive
> sub-labs, and append-only event history.

Five things follow from "inhabited":

1. **It has a self.** Every atomic-lab declares who it is in `IDENTITY.md`.
2. **It has a contract.** `CHARTER.md` says what it's allowed and not
   allowed to do.
3. **It has running state.** `STATE.md` records where it is, refreshed
   each session.
4. **It speaks asynchronously.** `inbox/` receives messages from the
   director; `outbox/` sends them. Both are flat directories of `.md`
   files.
5. **It remembers.** `events.log`, `journal/`, and `memory/` are three
   different kinds of long-term memory.

---

## The eight core directories

Every atomic-lab has the same eight directories (plus four top-level
`.md` files: CHARTER, IDENTITY, STATE, LABBOOK). The pattern is rigid
by design — predictability is the point.

```
<lab-name>/
├── CHARTER.md          mission, constraints, budget, approval rules
├── IDENTITY.md         role, voice, tools, what-it-is-not
├── STATE.md            running state, refreshed each session
├── LABBOOK.md          append-only running record of work — the lab's commit log
├── events.log          append-only timeline of lifecycle events (structured)
│
├── inbox/              messages FROM the director TO the lab
├── outbox/             messages FROM the lab TO the director
│
├── threads/            long-running open questions
│   └── <thread-name>/
│       ├── hypothesis.md
│       └── findings.md
│
├── experiments/        bounded one-shot tests with verdicts
│   └── <exp-name>/
│       ├── method.md
│       ├── results.md
│       ├── verdict.json
│       └── logs/
│
├── sublabs/            recursive nested labs (same eight-dir shape)
│   └── <sublab-name>/  (full atomic-lab structure, recursive)
│
├── memory/             reusable patterns lifted out of work
│   └── playbooks/      "do X this way" guides distilled from experience
│
├── journal/            stream-of-thought working notes
│
└── artifacts/          things the lab produces
    └── candidates/     candidates for promotion to higher-level tooling
```

---

## What goes in each piece

### `CHARTER.md` — the contract

Sections:
- **Set by:** who created the lab (almost always `director`)
- **Date:** birth date
- **Supersedes:** previous charter version (if any)
- **Mission:** one-paragraph statement of purpose
- **Immediate priority:** the very first concrete thing the lab should do
- **Constraints:** what the lab is NOT allowed to do without approval
  (spend, write actions, scope creep)
- **Success criteria:** how the lab knows the immediate priority is done
- **Open follow-ups:** known future threads, deferred not pursued
- **Budget for v0:** experiment count + dollar cap
- **Approval rules:** which actions require explicit director sign-off

Charters can be amended. Each amendment notes the previous version it
supersedes.

### `IDENTITY.md` — who the lab is

Sections:
- **First-person opening:** "I am the X lab. My job is …"
- **Mission:** restated in first person
- **Style:** how the lab thinks and acts (preferences, biases,
  read-only-by-default policy, voice sourcing)
- **Inherited context:** files outside the lab the lab needs to know
  about, with paths
- **Tools available:** CLIs, APIs, manual workflows
- **What I am NOT:** explicit boundary statements

Identity is **stable across sessions** — it's the lab's character, not
its current state.

### `STATE.md` — where the lab is right now

Sections:
- **Updated:** ISO 8601 timestamp of last refresh
- **Headline:** one-sentence summary of the lab's current situation
- **Open threads:** with their state (active / parked / closed)
- **Sub-labs:** what's nested and their status
- **Reports out:** outbox items still awaiting reply
- **Artifacts produced this session:** what was created
- **Capabilities now demonstrably has:** proven during the session
- **Capabilities NOT yet demonstrated:** known gaps
- **Budget:** experiments used / spend used vs. cap
- **Next move:** what happens when the lab next becomes inhabited

STATE.md is the **resume hand-off** — a fresh session reads STATE.md
and knows what to do.

### `events.log` — append-only history

One line per event. Format:

```
2026-05-02T20:15Z lab=<lab-name> event=<event-name> [key=value …]
```

Defined event kinds:
- `lab_born`
- `thread_opened name=<name>`
- `thread_parked name=<name> reason=<reason>`
- `thread_graduated name=<name> answer_via=<source>`
- `thread_closed name=<name>`
- `experiment_started exp=<name>`
- `experiment_concluded exp=<name> verdict=<kept|reverted|inconclusive> [blocker=<x>]`
- `decision_request_emitted id=<NNN> topic=<topic>`
- `director_decision payload=<short>`
- `sublab_spawned name=<name>`
- `report_emitted name=<name>`
- `report_received from=<source> name=<name> headline=<short>`
- `artifact_promoted name=<name> status=<candidate|graduated>`
- `playbook_captured name=<name> scope=<lab|parent_lab>`

This is a **closed vocabulary** for the system layer. Domain-specific
events (e.g. `deploy_started` in an ops-flavored lab) are allowed but
must be documented in the lab's CHARTER.

### `LABBOOK.md` — the running record

The lab's **commit log of its own work, written in human prose, in
order, append-only**. Each entry is a small unit of work that just
happened, recorded *as it happens*, not retrospectively. Reading
LABBOOK.md tail-to-head reconstructs how the lab got to its current
state.

Format: a markdown heading per entry with timestamp, then 1-3 sentences
in present-perfect or past tense. Short. No formatting beyond a heading
and a paragraph.

```markdown
## 2026-05-02T23:40Z
Identified root cause for the request-timeout regression — the worker
pool was being initialized before the config loader returned, so
in-flight requests landed on a pool with stale credentials. Fix
specced in exp-002 verdict; awaiting director approval.

## 2026-05-02T23:18Z
Ran exp-001 baseline measurement (N=3). Surfaced two concrete bugs in
the smoke stack: timeouts on the primary path and stale context on the
secondary. Both worth their own threads.

## 2026-05-02T23:00Z
Lab born. First reference instance. Environment set up with project
deps pinned per CHARTER §dependencies.
```

### LABBOOK.md vs. journal/ vs. events.log

The three persistence streams have different shapes:

| | Form | Cadence | Audience | Use to answer |
|---|---|---|---|---|
| `events.log` | Structured key=value lines | One per lifecycle event | Machines + audit | "When did X happen?" |
| `LABBOOK.md` | Markdown headings + 1-3 sentences | One per unit of work | Human picking up the lab cold | "What's been going on lately?" |
| `journal/` | Free-form markdown files | One per significant moment | Future supervisor sessions | "What was I thinking when I did this?" |

Rule of thumb:
- **events.log** = git's `--oneline` (machine-grepable)
- **LABBOOK.md** = git commit messages (the running log a human can scroll)
- **journal/** = a diary entry written when something deserves reflection

If you can't decide between LABBOOK and journal: **default to LABBOOK**.
A short entry with a timestamp is always correct. Journal entries are
for *occasions* — the lab being born, a thread graduating, a major
realization. Most work is just LABBOOK material.

### LABBOOK and git

If the lab directory is a git repo (or part of one), the **preferred
implementation** is to skip writing LABBOOK.md by hand and instead use
a post-task helper that commits the lab's working tree with a
synthesized commit message after each unit of work. Then
`git log -- <lab-path>` **is** the lab book. No separate file to
maintain, no risk of LABBOOK drifting from reality.

The synthesized commit message follows the same shape as a LABBOOK
entry — present-perfect, 1-3 sentences, the unit of work. Example:

```
labbook(<lab-name>): identify request-timeout root cause

Worker pool was being initialized before the config loader returned,
so in-flight requests landed on a pool with stale credentials. Fix
specced in exp-002, awaiting approval.
```

When LABBOOK.md exists alongside git history, treat the file as the
**authoritative source for entries that span pre-git or external
events** (e.g. a director conversation in another tool that informed
the next move). Most entries should be commits.

### `inbox/` — director → lab

Flat dir. The director writes `.md` files here. Lab reads them next
session and acts on them. Naming convention:
`response-NNN-<topic>.md` (a reply to outbox/decision-request-NNN) or
`directive-<topic>.md` (an unsolicited instruction).

### `outbox/` — lab → director

Flat dir. The lab writes `.md` files here when it needs the director's
attention. Naming conventions:
- `decision-request-NNN-<topic>.md` — a structured ask with options
- `<kind>-report-NNN-<topic>.md` — a finding the lab wants visible
- `<kind>-confirmation-<topic>.md` — confirmation of a completed action

The decision-request format follows a consistent shape: situation,
options (with `### A.`, `### B.`, …), recommendation, what-happens-next.

### `threads/<name>/` — long-running open questions

A thread is a question the lab is exploring that may take multiple
sessions or experiments to resolve. Files:
- `hypothesis.md` — what we think is true and why
- `findings.md` — appended each session with what was learned

A thread's state is one of:
- `open` — actively being worked
- `parked` — blocked on an external (token, decision, dependency)
- `graduated` — answered, often via a sub-lab
- `closed` — abandoned or no longer relevant

### `experiments/<name>/` — bounded one-shot tests

An experiment has a hypothesis, a method, runs once (per session),
produces a verdict. Files:
- `method.md` — steps + success criteria + cost/risk
- `results.md` — what actually happened
- `verdict.json` — structured outcome
- `logs/` — raw output captured during the run

Verdict structure:
```json
{
  "experiment_id": "...",
  "thread": "...",
  "run_at": "ISO 8601",
  "verdict": "kept|reverted|inconclusive",
  "score": {
    "quality": 0.0-1.0,
    "insight": 0.0-1.0,
    "leverage": 0.0-1.0
  },
  "critique": "what worked, what didn't, what we learned",
  "next_actions": ["..."],
  "blockers": ["..."]
}
```

Experiments end. Threads continue. Use the right shape.

### `sublabs/<name>/` — recursive nested labs

A sub-lab is a full atomic-lab nested inside another. It has the same
eight-dir structure, the same self-defining `.md` files, the same
events.log. The parent lab references the sub-lab in its STATE.md and
events.log.

When to spawn a sub-lab:
- The work is its own ongoing capability, not a one-shot question
  (so an experiment is wrong)
- The work warrants its own threads + experiments + memory
- The work is logically scoped to the parent (otherwise it's a sibling
  lab in `$ATOMICLAB_ROOT/`)

### `memory/` — distilled patterns

When the lab discovers a way of doing something that should be reused,
it lifts the pattern into `memory/playbooks/<name>.md`. A playbook is
a self-contained "how to do X" document, typically born from one
experiment but generalized.

Playbooks promoted further (to a higher-level runbook or CLI) leave a
record: events.log gets `artifact_promoted` or `playbook_captured`.

### `journal/` — reflective entries

Free-form markdown the lab writes when something deserves reflection
beyond a LABBOOK line. Not structured. Not required. Use for: lab
birth, thread graduation, a realization that reframes the work, an
honest "I was wrong about X" entry, a closeout on an experiment that
went deeper than the verdict captures.

If a moment can be expressed in 1-3 sentences, it's LABBOOK material.
If it wants paragraphs, voice, or argument, it's a journal entry.
Most entries should be LABBOOK; journal/ is where the lab has *taste*.

### `artifacts/` — produced things

Code, data, screenshots, JSON outputs. `artifacts/candidates/`
specifically holds things the lab thinks should be promoted (to a CLI
subcommand, to a runbook, to a higher-level tooling primitive).

---

## How a director uses an atomic-lab

A typical session:

1. **Read STATE.md** to find out where the lab is.
2. **Check `outbox/`** for any unanswered reports or decision-requests.
3. **Decide what's next.** Either:
   - Reply to an outbox item by writing to `inbox/`.
   - Open a new thread (and have the lab's supervisor work on it).
   - Spawn an experiment from an open thread.
4. **Watch the lab work.** Supervisor reads inbox, runs experiments,
   writes verdicts, updates STATE.md, logs to events.log.
5. **Receive new outbox items.** Read them, decide.
6. **Refresh STATE.md** at session end with the new headline + budget.

Asynchronous mode (deferred, see ROADMAP): the supervisor can also
work between director sessions, emitting outbox items. Director
catches up on the next visit.

---

## Out of scope for v0.1

These are deferred to later versions and intentionally NOT supported
yet:

- **Tick loop** — automated periodic invocation. Today the lab only
  runs when a director session opens it.
- **Coordinator** — a process that picks the next experiment to run
  given open threads + capacity. Today the director picks.
- **Parallel threads** — multiple threads progressing concurrently in
  one session. Today threads serialize on the director's attention.
- **Headless agent autonomy** — the lab driving its own LLM calls
  outside an attended session. Today every model call is in-session.
- **Inter-lab communication** — sibling labs reading each other's
  outbox. Today director relays explicitly.

These deferrals are not bugs. They're an explicit choice to nail the
inhabited-workspace shape before adding execution mechanics.
