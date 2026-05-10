# Lab Book — <TODO: lab-name>

Append-only running record of work, in human prose. Each entry is a
small unit of work that just happened.

Newest entries on top. Format: `## <ISO-8601 timestamp>` then 1-3
sentences, present-perfect tense.

If this lab's directory is a git repo (or part of one), prefer letting
git history serve as the lab book — the `bin/labbook-commit` helper
commits the working tree with a synthesized message after each unit
of work, and `git log -- <this-lab-path>` becomes the authoritative
record. Use this file for entries that don't naturally fit a commit
(director conversations elsewhere, observations between commits,
etc.).

See `ARCHITECTURE.md` (LABBOOK.md section) at the repo root for the
full spec.

---

## <TODO: ISO 8601 timestamp e.g. 2026-05-02T20:15Z>
Lab born. <TODO: one sentence about what just got set up.>
