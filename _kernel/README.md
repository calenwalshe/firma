# Atomic Lab Protocol

> A file-shaped framework for running structured research and engineering experiments. One operator, many threads, durable history.

> **🧪 EXPERIMENTAL — v0.1.0.** This is the public extraction of a pattern that has worked for one operator, on one machine, for a few weeks. **Stability is not promised. Conventions may change.** Treat this as a sketch you can borrow, not a product you can depend on.

---

## What is this?

Atomic Lab Protocol is a **convention** for how to lay out a working
directory so that a single operator (the "director") can run several
long-running concerns in parallel without losing the thread of any
of them.

It's three things:

1. **An eight-directory shape.** Every "atomic-lab" is a directory
   with the same eight subdirectories (`inbox/`, `outbox/`,
   `threads/`, `experiments/`, `sublabs/`, `memory/`, `journal/`,
   `artifacts/`) and the same four top-level markdown files
   (`CHARTER.md`, `IDENTITY.md`, `STATE.md`, `LABBOOK.md`) plus an
   append-only `events.log`. The shape is rigid by design — the
   director never has to wonder where state lives.

2. **A 15-event vocabulary.** Lifecycle events (`lab_born`,
   `thread_opened`, `experiment_concluded`, `decision_request_emitted`,
   …) are written as one-line entries to `events.log`. The vocabulary
   is closed at the system layer; domain-specific events are allowed
   but must be declared in the lab's charter.

3. **A file-async-over-chat protocol.** The director and the lab
   communicate by writing markdown files into `inbox/` and `outbox/`,
   not by typing into a chat surface. This makes the conversation
   durable, scannable, and survivable across sessions.

Plus one helper, `bin/labbook-commit`, that turns each unit of work
into a commit so `git log` *is* the lab book (per ADR-0003).

## Why?

Long-running concerns deserve their own structured home.

When work spans many sessions — a research project, a debugging
investigation, a piece of writing, a creative project — the things
that go wrong are: state is lost between sessions, decisions slip out
of memory, side-quests get tangled with the main thread, and "what
was I doing?" eats the first ten minutes of every resume.

The atomic-lab shape pushes back on all four. State is in `STATE.md`,
refreshed each session. Decisions are in `decision-request-NNN-*.md`
and their responses, durable. Side-quests are sub-labs or threads,
explicit. Resume is `STATE.md` + `outbox/` + `events.log` tail —
about a 60-second read.

It's a pattern you could implement on a sticky note. The protocol's
job is to make the convention legible enough that *the same operator
six weeks from now* knows what every file is for.

## Quickstart

```bash
# Clone
git clone <this-repo> ~/projects/atomic-lab-protocol
cd ~/projects/atomic-lab-protocol

# Make the helper runnable
chmod +x bin/labbook-commit

# Pick a directory to be your lab root and tell the helper about it
mkdir -p ~/labs && cd ~/labs && git init
export ATOMICLAB_ROOT=~/labs

# Scaffold your first lab
cp -r ~/projects/atomic-lab-protocol/template ~/labs/my-first-lab
cd ~/labs/my-first-lab

# Fill in CHARTER.md / IDENTITY.md / STATE.md (replace the <TODO:>s)
$EDITOR CHARTER.md IDENTITY.md STATE.md

# Birth event
echo "$(date -u +%Y-%m-%dT%H:%MZ) lab=my-first-lab event=lab_born" \
  >> events.log

# Commit it as the first lab-book entry
~/projects/atomic-lab-protocol/bin/labbook-commit my-first-lab
```

For a longer walkthrough, see [`docs/getting-started.md`](docs/getting-started.md).

## What this isn't

- **Not a project-management product.** No deadlines, no assignees,
  no Gantt charts.
- **Not a GUI.** Everything is markdown files and one shell helper.
- **Not an orchestration runtime.** There is no scheduler, no task
  queue, no agent loop. The director (a human, a CLI, an agent
  harness — whoever) is what advances work.
- **Not a methodology.** It doesn't tell you how to do science, how
  to ship code, or how to think. It only tells you where to put the
  files.
- **Not yet a stable protocol.** v0.1 is a single-operator extraction.
  Names, conventions, and event vocabulary may change before v1.0.

## Status

- **Version:** v0.1.0-experimental.
- **Tested by:** one operator, one machine, over a few weeks.
- **Not yet dogfooded** outside the original lab system this was
  extracted from — see [`ROADMAP.md`](ROADMAP.md) for what would have
  to be true to call it dogfooded.
- **Not yet recommended** for anyone who would be unhappy seeing
  conventions break under them.

## Contributing

Not yet accepting contributions.

If you try this out and learn something, raise a GitHub issue with the
shape `[finding] <one-line headline>` and a short description of what
you tried, what worked, what didn't. Issues are the primary signal we
care about right now.

PRs may be left open without merge for a while as the shape stabilizes.

## License

[MIT](LICENSE).
