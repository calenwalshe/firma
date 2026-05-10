---
id: 0001
date: {{LAUNCH_DATE}}
status: decided
parent_adr_refs: []
---

# ADR 0001 — Founding {{COMPANY_NAME}}

## Context

{{COMPANY_NAME}} is being founded to {{ONE_LINE_PURPOSE}}.

The founder(s) — {{FOUNDER_NAMES}} — have committed to the work shape
described in [`00-foundation/CHARTER.md`](../00-foundation/CHARTER.md).
This ADR captures the foundational decisions made at company creation,
so that a reader 18 months from now can recover the reasoning.

## Decision

Found {{COMPANY_NAME}} as a {{LEGAL_SHAPE}} in {{STATE_OF_FORMATION}}
on {{LAUNCH_DATE}}, under the following parameters:

- **Legal shape:** {{LEGAL_SHAPE}}.
- **State of formation:** {{STATE_OF_FORMATION}}.
- **Registered agent:** {{REGISTERED_AGENT}}.
- **Founders / owners:** {{FOUNDER_NAMES}}, with ownership split
  recorded in {{operating agreement | bylaws | partnership agreement}}.
- **Brand stance:** {{public-facing under company brand | founder-
  behind-brand stealth | parent-brand inheritance}}.
- **Domain:** {{DOMAIN}}.
- **Sunset condition:** {{time-bound | outcome-bound | 90-day disprove |
  no sunset (record reasoning below)}}.

## Consequences

- The company exists as a legal entity with the responsibilities and
  protections that {{LEGAL_SHAPE}} confers.
- The company files annual reports with {{STATE_OF_FORMATION}} on
  {{annual report date}}.
- Federal tax filing: {{Schedule C | 1065 | 1120 | 1120-S}}.
- The company opens a separate business bank account at
  {{BANK_NAME}}.
- The company maintains the corporate veil by following formalities
  appropriate to its shape (separate accounts, written ADRs for
  shape-changing decisions, annual minutes if a corp).
- IP-assignment is in place for every founder and contractor.
- The website (`{{DOMAIN}}`) carries the company brand, not any
  individual founder's name (unless brand stance overrides).

## Alternatives considered

- **{{ALTERNATIVE_LEGAL_SHAPE}}.** {{Why rejected.}} Common
  alternatives: a different legal shape (sole-prop instead of LLC,
  C-corp instead of LLC), a different state of formation (Wyoming or
  Delaware instead of home state), or no formation (operate
  informally as the founder personally).
- **No company at all** (do this work as a contractor / freelancer
  under personal name). {{Why rejected — usually because the
  liability shield of an entity is worth the formation cost, or
  because the work has more than one owner.}}
- **Spinning up a separate entity for each line of business**
  rather than one company doing multiple things. {{Why rejected —
  the seed assumes single-purpose; if the company has genuinely
  separate lines, consider this question explicitly.}}

## Why this over alternatives

{{2-3 sentences. The thing the founder would say to a stranger
reading this in 18 months who asks "why this?"}}

## Sunset reasoning (if §Sunset deleted from CHARTER)

{{If the company has elected to delete the §Sunset section from the
CHARTER, this section records why.

Common reasons:
- Established revenue / going concern that doesn't fit a 90-day clock.
- Multigenerational family business shape.
- Long-cycle work where 90 days is the wrong unit.

Document the reason. The forcing function still applies — what's the
quarterly review cadence, and what triggers a serious "do we keep
going?" check?}}

## Cross-references

- CHARTER: [`../00-foundation/CHARTER.md`](../00-foundation/CHARTER.md)
- Legal posture: [`../10-legal/README.md`](../10-legal/README.md)
- Banking and books: [`../20-financial/README.md`](../20-financial/README.md)
