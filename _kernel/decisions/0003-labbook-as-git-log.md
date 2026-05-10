# ADR 0003 — The lab book is the git log

**Status:** accepted
**Date:** 2026-05-03

## Context

Atomic-labs accumulate state across sessions. We have three persistence
streams already (ADR 0001):

- `events.log` — structured one-line-per-event audit trail
- `journal/` — free-form reflective writeups at significant moments
- `STATE.md` — point-in-time snapshot, rewritten

There's a missing layer: **the running record of work as it happens.**
A line-by-line "here's what I just did" stream that lets a fresh
session read backwards and reconstruct context cheaply.

A first sketch added `LABBOOK.md` as a hand-maintained markdown file
for this. The director observed: "doesn't it make sense for a lab to
use a hook to commit after each set of work was done and create a
commit message based on it so we can reconstruct the chain?"

That observation is right. Hand-maintained markdown decays. Git
commits don't, because they require an explicit action (`git commit`)
and the act of committing can be wired to other lab events.

## Decision

**The lab book is `git log`.** Specifically:

1. **One git repo per lab root.** The directory pointed at by
   `$ATOMICLAB_ROOT` is a single git repo. Each lab is a subdirectory.
   `git log -- <lab-name>/` is that lab's running record. Cross-lab
   queries via plain `git log`. (The choice between one shared repo
   vs. per-lab repos is discussed in *Considered alternatives*; the
   shared repo is the recommended default.)

2. **A unit of work ends with a commit.** The same triggers that
   append to `events.log` should also commit. Concretely:
   experiment_concluded, thread_opened, thread_parked, thread_graduated,
   thread_closed, decision_request_emitted, director_decision applied,
   sublab_spawned, playbook_captured, artifact_promoted.

3. **A passive helper, not an active hook.** A `labbook-commit` CLI
   that the lab supervisor invokes when a unit of work is done.
   Reasons:
   - Active hooks (e.g. an agent-harness "Stop" event) commit half-done
     work because "the agent paused" doesn't equal "work unit
     finished."
   - Passive helpers preserve the invariant that "every commit is a
     coherent unit," which is what makes `git log` valuable as a
     record.
   - Lower blast radius. If the helper is buggy, a manual `git commit`
     still works; if an active hook is buggy, every agent turn
     produces noise.

4. **Commit message synthesis is pluggable; the default is the diff
   stat.** Helper takes the staged diff (`git diff --cached --stat`),
   the last N lines of the lab's `events.log`, and the most recent
   file in `outbox/` if present. By default, the helper assembles a
   conventional-commit subject from those inputs without calling out
   to a model — `labbook(<lab-name>): <staged file count> files / <N>
   lines changed`. Operators who want richer messages can plug in
   their own LLM provider (the helper exposes a model hook). The
   model choice is not part of the protocol.

5. **Conventional-commit prefix.** `labbook(<lab-name>): <subject>`.
   Lets `git log --grep='^labbook('` slice all lab activity and
   `git log --grep='^labbook(<name>)'` slice one lab.

6. **LABBOOK.md remains as a stub.** The file in each lab is now an
   index pointing to git, not the canonical record. It exists for
   external-event entries that didn't go through git (e.g. a
   conversation that informed the next move but produced no commit).

## Considered alternatives

### Per-lab repos (`<lab-name>/.git`)
Cleanest mental model — each lab IS its history. Trade-off: cross-lab
`git log` becomes awkward (you have to walk subrepos), and tooling
that wants a single timeline has to merge across repos. For
single-operator setups, the shared repo wins on simplicity. For team
or distribution scenarios, per-lab repos may be preferable.

### Project-level repo (lab dir tracked alongside everything else)
Track labs alongside everything else in some larger project repo.
Trade-off: history pollution — the project's commit log fills with
lab churn — and the lab's git history becomes intermixed with
unrelated work. Recommend a dedicated `$ATOMICLAB_ROOT` repo.

### Active commit hook on every agent turn
Auto-commit the working tree whenever the agent harness fires its
"turn complete" event. Rejected: not every agent pause is a unit of
work boundary. Risk of partial-work commits is high.

### Hand-maintained LABBOOK.md only
Markdown file the supervisor edits. Rejected: discipline-dependent.
The first sessions to try this demonstrated the failure mode — entries
got written when convenient, not consistently after each unit of
work.

### LLM-synthesized commit messages as the default
Higher-quality subjects, at the cost of binding the protocol to a
model provider and an API key. Useful as an opt-in feature; not
useful as a default. The protocol should run on a fresh laptop with
nothing but `git`.

## Consequences

### Positive
- `git log -- <lab-name>` becomes the canonical history. No separate
  file to keep in sync with reality.
- Diffs are inherent in the record (every commit shows what changed).
- Cross-lab archeology becomes trivial via standard git tooling.
- Commit messages auto-link to events.log by sharing trigger
  vocabulary.
- Reversibility: bad commit can be reverted; bad hand-edits to a file
  required surgical rewriting.

### Negative
- Requires the lab supervisor to call `labbook-commit` after each unit
  of work. New discipline, will take a few sessions to feel natural.
- Pre-LABBOOK history is captured in an initial checkpoint commit;
  granular history starts after this ADR lands in your environment.

### Neutral
- LABBOOK.md still exists in each lab but is now mostly a pointer.
  Future ADR might remove it entirely once the pattern proves out.

## Implementation

- `bin/labbook-commit` — Python helper. Stages everything in the lab
  dir, builds a default commit message from the diff stat + last N
  events.log lines, commits. Exposes `--message` / `--subject`
  overrides for hand-written commits and a model hook for plug-in
  synthesis.
- `ARCHITECTURE.md` reflects the LABBOOK.md → git log shift.

## Revisit when

- Lab activity is high enough that manual `labbook-commit` discipline
  fails (then revisit active-hook with stricter "is this really done?"
  signal — probably the events.log writer triggers it).
- Cross-lab git operations get awkward (then revisit per-lab repos).
- The default message synthesis becomes the bottleneck (then revisit
  whether the helper should ship with a default LLM integration).
