---
layer: brand
status: template
---

# Brand — Name, identity, mark, domain

The default brand stance for this seed: the company has its own brand,
distinct from any one founder's name. Edit if your stance is
otherwise (founder-led brand, parent-brand inheritance, brand-stealth
opt-in).

---

## Name

The company's name is a load-bearing artifact. A real name carries:

- **A story.** What does the name mean? Why was it chosen? (1-2
  sentences. Plain. "Northbridge" came from the bridge that connects
  the firm's neighborhood to downtown — small, structural, named for
  the actual geography we serve.)
- **A register.** Is it formal? Playful? Technical? Match the customer
  you serve.
- **A trademark posture.** Is the name searchable and clearable? Have
  you done a USPTO TESS search ([tmsearch.uspto.gov](https://tmsearch.uspto.gov))?
- **A domain.** Is the .com available? If not, are you OK with
  a `.co`, `.io`, `.law`, `.dev` alternative?

### Sketch the name story here

> {{COMPANY_NAME}} — {{2–3 sentences: what does the name mean, why
> was it chosen, what register does it carry.}}

### USPTO TESS search

- **Done?** {{YES, on YYYY-MM-DD | DEFERRED — venture is small enough
  that a future rename is acceptable.}}
- **Filing:** {{NOT FILED | INTENT-TO-USE FILED on YYYY-MM-DD |
  REGISTERED on YYYY-MM-DD.}}

A formal trademark filing costs ~$250–$350/class via USPTO + ~$500–
$1,500 in attorney fees if you use one (Cooley, LegalZoom, Trademarkia,
or a solo trademark attorney). Skip filing at v0; revisit when the
brand has visible value to protect.

---

## Domain

- **Primary:** {{DOMAIN.com}}
- **Held but not active:** {{secondary TLDs — .ai, .co, .org, .law,
  .dev, depending on the field — or "none"}}
- **DNS:** Cloudflare (default — free, fast, full control).
- **Hosting:** Cloudflare Pages / Vultr / Netlify / Vercel — pick what
  matches your engineering shape.

### Why Cloudflare for DNS

Free, fast, no DNS upcharge from your registrar. If you registered
the domain elsewhere, you can transfer to Cloudflare Registrar (free,
at-cost pricing) or just use Cloudflare DNS by changing nameservers.

---

## Social handles

Claim handles on instantiation even if you don't plan to use them at
v0 — name-squatting protection is cheap.

| Platform | Handle | Status |
|---|---|---|
| Twitter / X | {{@HANDLE}} | {{claimed | not yet}} |
| LinkedIn | {{HANDLE}} | {{claimed | not yet}} |
| GitHub | {{github.com/HANDLE}} | {{claimed | not yet}} |
| {{other relevant platform}} | | |

---

## Visual identity

The seed ships a "no brand yet" placeholder palette so you can be
shipping copy and pages while the visual identity is unfinished:

- **Primary color:** warm-black `#1a1a1a`
- **Background:** off-white `#fafafa`
- **Accent:** one accent color of your choice (default for
  uninflected: muted slate-blue `#4a6b8a`).
- **Typography:**
  - Sans-serif (body): Inter
  - Monospace (code, tables): IBM Plex Mono
  - Display (headings, marketing): Playfair Display
- **Spacing:** 8-point grid (8 / 16 / 24 / 32 / 48 / 64).

This default works for a law firm or a creative agency or a SaaS — it
is intentionally bland, intentionally legible, intentionally not
distinct. When you have a real brand, replace this section.

If your company has no visual surface yet (you sell APIs, reports,
services without a designed UI), say so:

> No visual surface at v0. The company sells {{API access | reports |
> services}} that don't require a designed interface. Visual identity
> will land when there's a customer-facing surface that needs one.
> Until then, the brand lives in the name, the voice, and the domain.

---

## Voice

Inheriting a thoughtful default voice while you decide your own:

**The "uninflected" default:**

- **Plain.** No jargon. No buzzwords. Read what you wrote out loud; if
  it sounds like a press release, rewrite.
- **Declarative.** Make claims. Avoid hedging ("might", "could",
  "potentially") unless you're genuinely uncertain.
- **No exclamation points.** None. Not "!!". Not even one. The
  exclamation point in marketing copy reads as desperate or as if
  speaking to someone half-asleep.
- **Second-person direct** in product and customer-facing copy ("you").
- **First-person plural** for the company's own voice ("we").

**Banned phrases (the "uninflected" base list):**

- "We are excited to announce…"
- "Game-changer."
- "Disrupting…"
- "Best-in-class."
- "Cutting-edge."
- "Leverage" (as a verb meaning "use").
- "Solutions" (used as a vague catch-all noun for "things we sell").
- "World-class."

Add to this list as the company earns specific bans (phrases that
matter for your industry's failure modes).

### When to override the default

- **Consumer-facing product company?** May want a warmer, more
  conversational register. The bans still apply.
- **Licensed-profession firm (law, medicine)?** Want a more formal
  register, longer sentences, more cautious hedging where the
  profession requires it.
- **Creative agency, design studio?** Voice is part of the product;
  the default is too plain, write your own.

---

## Brand stance — public-or-stealth

Most companies use their own brand in public; the founder appears
under their own name where the field calls for it (lawyers, doctors,
consultants).

If your stance is **founder-behind-brand** (the founder's name doesn't
appear on public output), document why — this is non-default:

- Stealth-from-an-employer (the founder has a day job whose conflict
  policy or similar arrangement keeps them off public surfaces).
- Privacy / safety reasons.
- The brand is genuinely larger than the founder and the founder
  doesn't want to be the public face.

If founder-behind-brand applies, also add an ADR in
`decisions/0002-brand-stance.md` recording the choice and the
specific surfaces it applies to (LinkedIn? email signatures?
contracts?).

---

## What goes in `assets/`

When you have real brand assets, this directory holds:

- `logo.svg` — the canonical mark.
- `logo-favicon.png` (32x32, 64x64).
- `og-card.png` — 1200x630 social sharing card.
- `colors.md` — full palette, including grays and semantic colors.

The seed ships nothing here at v0. Ship a logo when you have one.

---

## Graduation path

When the brand layer outgrows one file:

```
30-brand/
├── README.md
├── IDENTITY.md                # palette, type, mark spec
├── VOICE.md                   # extended voice rules + examples
├── domain-checklist.md
├── og-card.py                 # generation script
└── assets/
    ├── logo.svg
    ├── logo-favicon.png
    └── og-card-template.png
```

Add as you earn it.
