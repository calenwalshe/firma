---
layer: comms
status: template
---

# Comms — Internal, external, customer

Three audiences, three channel-stacks, one set of rules.

This layer names where messages flow and who reviews them before
they go out. Edit to fit your company's actual shape; delete the
sections that don't apply.

---

## Posture

Comms-layer principles that hold across all three audiences:

1. **Public claims are commitments.** What you put on the website,
   in marketing copy, on social is a promise. Don't claim certifications
   you don't have, capacities you can't deliver, or testimonials you
   can't substantiate.
2. **Customer-facing outbound that goes out at scale gets reviewed.**
   Whether by a person or by a documented automated check, every
   bulk-outbound surface (email blast, mass-DM, press release, ad
   creative) goes through review. The review may be the founder
   reading it once. It is not zero.
3. **Audit what was sent.** Keep a record of customer-facing comms
   that went out — at minimum, the timestamp, the channel, who sent
   it, and the recipient or audience. For ~80% of small companies
   the email-archive in your inbox + your CRM are sufficient.

---

## Internal — how the team talks to itself

For a 1-person company: skip.

For 2–5 people:

- **Email + in-person + occasional video calls.** No dedicated chat
  tool needed. Slack/Discord is overhead at this scale.
- **Shared docs:** Google Workspace or Microsoft 365 is the default;
  Notion or Coda for teams that lean toward structured-page workflows.
- **Decisions get written down.** ADRs in `decisions/` are the
  durable record. Don't let the source of truth be a Slack thread.

For 5–10 people:

- **Add a chat tool** (Slack, Discord, Microsoft Teams) when message
  volume justifies. Pick one — don't run two.
- **Calendar:** Google Calendar or Outlook, with a shared team
  calendar for milestones, time-off, and recurring rituals.
- **Async-first cadence:** weekly written status from each person;
  one short live meeting per week max. Resist the drift to daily
  standups until the team genuinely needs them.

For >10 people: this layer outgrows the seed. Fork to a fuller stack.

---

## External — how the company talks to the world

### Website

Single-page is enough at v0. The "{{company}}/website-skeleton/"
graduation pattern (deferred) gives a static-HTML scaffold with:

- Hero (one line: what the company does).
- Three sections at most (offer, proof, contact).
- A `help@` contact link.
- A privacy policy and terms link (deferred to `90-operations/`).

Default hosting: Cloudflare Pages / Netlify / Vercel — all free for
small-traffic sites. Don't run a CMS at v0; raw HTML or a static-site
generator (Eleventy / Hugo / Astro) is enough.

### Email

- **`<founder>@<domain>`** — your personal address at the company.
- **`hello@<domain>`** or **`info@<domain>`** — generic catch-all
  forwarding to the founder.
- **`help@<domain>` or `support@<domain>`** — customer support alias.
- **`legal@<domain>` or `notices@<domain>`** — for legal notices
  (DMCA, regulatory). Set up when you have a public surface.

Provider:

- **Google Workspace** ($7/user/month). Default for most companies.
- **FastMail** ($5/user/month). Default for privacy-leaning founders.
- **Microsoft 365** ($6+/user/month). Default if you're already deep
  in the Office ecosystem.

### Social

Pick at most two platforms at v0. Where your customers actually are:

- **B2B service / professional:** LinkedIn primary; Twitter/X if you
  publish writing.
- **B2C product:** Instagram + TikTok + (maybe) Facebook.
- **Developer-tooling / open-source:** Twitter/X + GitHub primary;
  LinkedIn secondary.
- **Local services:** Google Business Profile (free, important) +
  Instagram or Facebook depending on locale.

If you're not going to post at least monthly, claim the handle and
don't pretend it's an active surface. An empty social handle is fine;
a stale one looks worse than absent.

### Press / outbound

Press outreach (sending pitches, responding to journalist inquiries)
is its own discipline. At founding, expect to do zero of this. When
you have a story worth telling, write it once on your own surface
(blog post, email to your list) before pitching anyone.

---

## Customer — how the company talks to people who pay

### Support channel

Default at v0: **`help@<domain>`** alias, forwarded to the founder
inbox, with a 24-hour response SLA on weekdays. That's it.

You don't need:
- A help-desk product (Zendesk, Intercom, Front, Help Scout) until
  ticket volume justifies it. Most small companies don't reach that
  point until ~$100k+ MRR or ~50+ customers.
- A chatbot.
- A phone line (some service businesses do; most product companies
  don't until much later).

### Outbound to customers

Three categories, three review patterns:

1. **One-to-one:** founder writes, founder sends. No review gate
   beyond the founder's own judgment.
2. **One-to-many transactional** (receipts, password resets,
   confirmations): templated, sent automatically by your billing /
   product / email service. Test the template; review only when
   the template changes.
3. **One-to-many announcements** (product updates, newsletters,
   marketing emails): drafted, reviewed, sent. The review can be
   another founder or a trusted advisor; for a solopreneur, it can
   be a 24-hour cool-off ("write it, sleep on it, send tomorrow").

### Contracts and legal-shaped communication

Anything that creates an obligation or a right (engagement letters,
SOWs, NDAs, settlement language): drafted by the founder, reviewed
by counsel before first send. Once you have a reviewed template,
subsequent uses can go out without re-review unless the language
changes.

Don't draft your own NDA from scratch. Use a template, modify
sparingly.

---

## What this layer is NOT

- A help-desk replacement. (Use Zendesk / Front / Help Scout when
  volume justifies; the seed names the posture, not the product.)
- A marketing-automation playbook. (Different layer if you ever build
  one out — typically inside `70-sales/` for outbound; here for the
  posture only.)
- A crisis-comms playbook. (Lives in `90-operations/incident-response.md`
  when you build it.)

---

## Graduation path

When this layer outgrows one file:

```
40-comms/
├── README.md
├── COMMS-PROTOCOL.md          # full posture + audit policy
├── website-skeleton/
│   ├── index.html
│   └── style.css
├── email-setup.md             # provisioning + alias setup
├── support-shape.md           # SLA + ticket flow when help-desk lands
└── inbound-form.md            # Tally / Typeform / hand-rolled
```

Add as you earn it.
