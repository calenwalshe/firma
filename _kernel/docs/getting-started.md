# Getting started with the Atomic Lab Protocol

> **Audience:** a single operator running long-running concerns
> (research, debugging, creative work, engineering) who wants a
> structured place to keep them.

---

## 1. Install

```bash
git clone <this-repo> ~/projects/atomic-lab-protocol
chmod +x ~/projects/atomic-lab-protocol/bin/labbook-commit
```

No Python deps for the default code path. The helper is a single
~200-line script that uses `git` and the standard library.

For LLM-synthesized commit messages, point `ATOMICLAB_SYNTH` at a
Python module exposing a `synthesize(...)` function. The protocol
does not bind you to a provider.

## 2. Choose a lab root

One directory, one git repo, multiple labs as subdirectories:

```bash
mkdir -p ~/labs
cd ~/labs && git init
export ATOMICLAB_ROOT=~/labs   # add to shell profile
```

The helper reads `$ATOMICLAB_ROOT`; if unset, it walks up from `cwd`
looking for a `.git`.

## 3. Scaffold your first lab

```bash
cp -r ~/projects/atomic-lab-protocol/template ~/labs/my-first-lab
cd ~/labs/my-first-lab
```

You now have:
- Three top-level docs: `CHARTER.md`, `IDENTITY.md`, `STATE.md`
- An empty `LABBOOK.md` (skip if using git-as-labbook from ADR-0003)
- An empty `events.log`
- Eight directories: `inbox/`, `outbox/`, `threads/`, `experiments/`,
  `sublabs/`, `memory/`, `journal/`, `artifacts/`

`CHARTER.md` is the contract: what this lab is allowed to do, what's
deferred, what its budget is. If you can't write a good charter, you
don't have a lab — you have a half-thought.

`IDENTITY.md` is who the lab is, in first person. Stable across
sessions.

`STATE.md` is where the lab is right now. Refresh every session.

## 4. Birth the lab

```bash
echo "$(date -u +%Y-%m-%dT%H:%MZ) lab=my-first-lab event=lab_born" \
  >> events.log
~/projects/atomic-lab-protocol/bin/labbook-commit my-first-lab
```

The `events.log` line is the canonical record; the commit is the
labbook entry for the same event.

## 5. The 15 events at a glance

Use these in `events.log`. Domain-specific events are allowed but
must be declared in CHARTER.

```
lab_born
thread_opened name=<name>
thread_parked name=<name> reason=<r>
thread_graduated name=<name> answer_via=<source>
thread_closed name=<name>
experiment_started exp=<name>
experiment_concluded exp=<name> verdict=<kept|reverted|inconclusive>
decision_request_emitted id=<NNN> topic=<topic>
director_decision payload=<short>
sublab_spawned name=<name>
report_emitted name=<name>
report_received from=<source> name=<name> headline=<short>
artifact_promoted name=<name> status=<candidate|graduated>
playbook_captured name=<name> scope=<lab|parent_lab>
lab_completed   (or: lab_abandoned reason=<r>, lab_reopened reason=<r>)
```

See `ARCHITECTURE.md` for full vocabulary; `LIFECYCLE.md` for the
state machine.

## 6. Your first thread + experiment

Threads are long-running open questions. Experiments are bounded
one-shot tests.

```bash
mkdir -p threads/my-first-thread
$EDITOR threads/my-first-thread/hypothesis.md
echo "$(date -u +%Y-%m-%dT%H:%MZ) lab=my-first-lab event=thread_opened name=my-first-thread" >> events.log

mkdir -p experiments/exp-001
$EDITOR experiments/exp-001/method.md
echo "$(date -u +%Y-%m-%dT%H:%MZ) lab=my-first-lab event=experiment_started exp=exp-001" >> events.log

# ...do the work, then write results.md and verdict.json...

echo "$(date -u +%Y-%m-%dT%H:%MZ) lab=my-first-lab event=experiment_concluded exp=exp-001 verdict=kept" >> events.log
~/projects/atomic-lab-protocol/bin/labbook-commit my-first-lab
```

After each unit of work, run `labbook-commit`. The git log becomes
the lab book.

## 7. When NOT to use this

- Single-session work — just open a file.
- Work where state IS the code — a regular project repo is fine.
- Multi-operator collaboration — the protocol is single-director by
  design; don't fight it.

If the lab feels heavier than the work warrants, it probably is.
Drop back to a directory and a notes file.

## 8. What next

- [`PROTOCOL.md`](../PROTOCOL.md) — inbox/outbox conventions.
- [`LIFECYCLE.md`](../LIFECYCLE.md) — lab state machine.
- [`decisions/0003-labbook-as-git-log.md`](../decisions/0003-labbook-as-git-log.md)
  — why commits are the lab book.

If a convention doesn't fit your work, file an issue. Conventions
will move at v0.2.
