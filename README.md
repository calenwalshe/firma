# firma

Templates for organizing complex projects.

A scaffold of file-shaped patterns — decision logs, context records,
artifact archives, layered concerns — that turn a tangled effort into
something a single person can navigate, hand off, or come back to in
six months.

Useful for anyone running a complex piece of work that needs decisions
tracked, context preserved, and artifacts kept where they can be
found: a 6-month research project, a multi-collaborator engineering
effort, a freelance practice you want to keep organized, a small
operation with several moving parts, an ongoing investigation. Sized
for 1–10 people.

Layered: a core R&D kernel for structured investigation (vendored at
[`_kernel/`](./_kernel)), plus a stack of scaffolding folders for the
operational concerns most complex projects eventually grow into.
Markdown + simple file shapes; no app to install, no service to run.
MIT.

---

## What's in here

```
00-foundation/    What this workspace IS — bedrock docs (CHARTER, PRINCIPLES)
10-legal/         Formal-shape paperwork, if the project has one
20-financial/     Money in / money out, if the project handles any
30-brand/         Name, identity, mark, domain
40-comms/         Internal + external + counterparty communication
50-decisions/     ADR pattern + how this workspace decides
60-team/          Roles + responsibilities + IP-assignment, if multi-person
70-sales/         Pipeline + agreements + billing, if revenue-bearing
80-product/       Spec + roadmap + release pattern, if something ships
90-operations/    Vendors + insurance + compliance + incident response
decisions/        Append-only ADR log (yours, not the scaffold's)
examples/         Worked examples — fully filled-in synthetic instances
_kernel/          R&D layer — vendored alongside the scaffold
```

Each folder is independently optional. Delete the ones a given
workspace doesn't need; the rest still work.

---

## Quickstart (~15 min read, ~1 hour to set up)

1. **Fork** or `gh repo create` from this template.
2. **Read** [`BOOTSTRAP.md`](BOOTSTRAP.md) end-to-end.
3. **Pick** which layers you actually need (most workspaces don't
   need all nine on day one).
4. **Find-and-replace** the `{{PLACEHOLDER}}` tokens.
5. **Delete** the layers that don't apply.
6. **Sign** [`decisions/0001-founding.md`](decisions/0001-founding.md)
   — the first entry in your decision log.
7. The R&D kernel is already vendored at [`_kernel/`](./_kernel) — no
   extra setup required. See [`_kernel/README.md`](_kernel/README.md)
   for when to spawn your first lab.
8. **Use it.**

A worked example (a fictional one-person artisanal-salt operation in
Maine) is at [`examples/salt-cellar-provisions.md`](examples/salt-cellar-provisions.md)
— one pattern; instantiate the scaffold differently for a research
project, a service practice, a side build, or anything else.

---

## Design principles

- **Generic by default, specific by edit.** Every file is a template.
- **Shape-neutral.** Works for a solo workspace, a partnership, a
  small team, a research group, a freelance practice; pick the
  shape at setup.
- **Size-neutral 1–10 people.** Templates assume the small case but
  don't break at 10.
- **Default-sane choices** in every layer; documented "why this
  default" and "when to swap."
- **Markdown + simple bash + standard formats** — non-engineers can
  read and edit every artifact.
- **Required field: a sunset condition.** Every workspace declares
  what would make it correct to stop. A 90-day disprove clock by
  default for pre-result work, or an explicit ADR-recorded reason to
  delete the §Sunset section. The scaffold will not let you set up
  something with no exit.
- **MIT licensed.** Fork freely. No phone-home.

---

## What this is not

- **Not a project-management product.** No issue tracker, no Gantt,
  no assignees. The artifacts are markdown files in a git repo.
- **Not a no-code wizard.** You write, not click.
- **Not a substitute for domain-specific advice.** Layers like
  `10-legal/` and `20-financial/` point at sane starting positions;
  high-stakes decisions still need a professional.
- **Not a complete workflow for any one shape.** It's a scaffold
  that gets the structure in place; the project itself is what fills
  it in.

---

## License

MIT. See [`LICENSE`](LICENSE). Fork without attribution if you want;
attribution appreciated if you find it useful.
