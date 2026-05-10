# Changelog

All notable changes to this project will be documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/), and
this project adheres to [Semantic Versioning](https://semver.org/) once
it reaches v1.0. Until then, breaking changes may land in any minor
version.

## 0.1.0 (2026-05-05) — initial experimental extraction

Patterns extracted from a single-operator lab system. Conventions may
change before v1.0.

### Included
- The eight-directory shape (`inbox/`, `outbox/`, `threads/`,
  `experiments/`, `sublabs/`, `memory/`, `journal/`, `artifacts/`)
- Top-level docs: `CHARTER.md`, `IDENTITY.md`, `STATE.md`,
  `LABBOOK.md`, `events.log`
- 15-event closed vocabulary (see `ARCHITECTURE.md`)
- File-async-over-chat protocol (`PROTOCOL.md`)
- Lifecycle state machine (`LIFECYCLE.md`)
- Three ADRs: 0001 (eight-dir contract), 0002 (files-not-chat),
  0003 (labbook-as-git-log)
- `bin/labbook-commit` — passive commit helper, default synthesis
  is deterministic (no LLM); pluggable via `ATOMICLAB_SYNTH`
- `template/` scaffold + `docs/getting-started.md`

### Known limitations
- Single-operator only. Multi-director coordination is unspecified.
- No tick loop / async runtime — labs only advance when the director
  attaches.
- Not yet dogfooded outside the original system this was extracted
  from.
- Names of events, dirs, and ADRs are likely to be revisited at v0.2.
