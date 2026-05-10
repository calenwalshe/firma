# firma

Generic company-class governance seed. Experimental.

A starter for spinning up a real company. Pairs with [`_kernel/`](./_kernel)
(the R&D layer, vendored alongside the seed) and ships templates for the
nine company-infrastructure layers: legal, financial, brand, comms,
decisions, team, sales, product, operations.

Works for a 1-person freelance shop, a 3-lawyer firm, a creative
agency, an early-stage SaaS, a coffee chain. Sized for 1–10 people;
past 10, fork to a fuller stack.

> **Not legal, financial, or tax advice.** The seed ships templates and
> sane defaults. For high-stakes calls (raising capital, hiring W-2
> employees in multiple states, regulated industries, IP licensing),
> retain counsel.

---

## What's in here

```
00-foundation/    What the company IS — bedrock docs (CHARTER, PRINCIPLES)
10-legal/         Entity formation + day-1 paperwork (LLC / C-corp / LLP / sole-prop)
20-financial/     Bank, books, taxes, runway
30-brand/         Name, identity, mark, domain
40-comms/         Internal + external + customer comms
50-decisions/     ADR pattern + how this company decides
60-team/          Hiring + roles + IP-assignment
70-sales/         Pipeline + contracts + billing
80-product/       Spec + roadmap + release pattern
90-operations/    Vendors + insurance + compliance + IR
decisions/        Append-only ADR log (your company's, not the seed's)
examples/         Worked examples — fully filled-in synthetic ventures
_kernel/          R&D layer — vendored alongside the seed
```

---

## Quickstart (~15 min read, 1–2 weeks calendar to be a real company)

1. **Fork** or `gh repo create` from this template.
2. **Read** [`BOOTSTRAP.md`](BOOTSTRAP.md) end-to-end.
3. **Pick** your legal shape ([`10-legal/README.md`](10-legal/README.md)).
4. **Find-and-replace** the `{{PLACEHOLDER}}` tokens.
5. **Delete** layers that don't apply (e.g. delete `80-product/` if you're
   a pure service firm with no product, or `60-team/` if you're a
   solopreneur committed to staying solo).
6. **Sign** [`decisions/0001-founding.md`](decisions/0001-founding.md).
7. The R&D kernel is already vendored at [`_kernel/`](./_kernel) — no
   extra setup required. See [`_kernel/README.md`](_kernel/README.md) for
   when to spawn your first lab.
8. **Ship.**

A worked example (a fictional one-person artisanal salt e-commerce in
Maine) is at [`examples/salt-cellar-provisions.md`](examples/salt-cellar-provisions.md).

---

## Design principles

- **Generic by default, specific by edit.** Every file is a template.
- **Legal-entity-neutral.** LLC / C-corp / LLP / sole-prop all
  supported; founder picks at bootstrap time.
- **Size-neutral 1–10 people.** Templates assume the small case but
  don't break at 10.
- **Default-sane choices** in every layer; documented "why this
  default" and "when to swap."
- **Markdown + simple bash + standard formats** — non-engineers can
  read and edit every artifact.
- **Required field: a sunset condition.** A 90-day disprove clock for
  pre-revenue ventures, or an explicit ADR-recorded reason to delete
  the §Sunset section. The seed will not let you scaffold a zombie.
- **MIT licensed.** Fork freely. No phone-home.

---

## What this is not

- **Not a project-management product.** No issue tracker, no Gantt,
  no assignees.
- **Not a no-code wizard.** The artifacts are markdown; you write,
  not click.
- **Not a venture studio playbook.** The seed is for the company you
  are starting, not for a portfolio of others.
- **Not a regulated-industry stack.** Healthcare with PHI, broker-dealer,
  fintech with deposit-taking, insurance: the seed gets you to "real
  company" but you'll need industry-specific counsel and tooling on top.
- **Not VC-ready as-shipped.** The seed gets a company to seed-stage
  ready; for venture-funded growth you'll layer cap-table software
  (Carta / Pulley), a 409A, and proper board governance on top.

---

## License

MIT. See [`LICENSE`](LICENSE). Fork without attribution if you want;
attribution appreciated if you find it useful.
