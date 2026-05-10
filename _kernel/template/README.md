# <TODO: lab-name>

This is the atomic-lab template. Copy it to start a new lab:

```bash
# $ATOMICLAB_ROOT points at the directory containing all your labs
cp -r template "$ATOMICLAB_ROOT/<your-lab-name>"
```

Then fill in the `<TODO:>` placeholders in:

- `CHARTER.md` — what the lab is allowed to do
- `IDENTITY.md` — who the lab is
- `STATE.md` — current state (will be refreshed each session)

After filling in, log the birth event:

```bash
echo "$(date -u +%Y-%m-%dT%H:%MZ) lab=<your-lab-name> event=lab_born" \
  >> "$ATOMICLAB_ROOT/<your-lab-name>/events.log"
```

For the full system architecture and conventions, see `ARCHITECTURE.md`,
`PROTOCOL.md`, and `LIFECYCLE.md` at the repo root.

## Eight-dir shape

The template ships with the canonical eight directories:

- `inbox/` — director → lab messages
- `outbox/` — lab → director messages (decision-requests, reports)
- `threads/` — long-running open questions
- `experiments/` — bounded one-shot tests with verdicts
- `sublabs/` — recursive nested labs
- `memory/` — distilled patterns (playbooks/)
- `journal/` — stream-of-thought working notes
- `artifacts/` — produced things (candidates/ for promotion)

Per ADR-0001 of the atomic-lab system, all eight dirs are required for
every atomic-lab. Empty is fine; missing is not.
