# Examples

**Examples deferred to v0.2 — pending dogfood. See
[`../ROADMAP.md`](../ROADMAP.md).**

This directory will hold worked examples of atomic-labs. It is empty
on purpose at v0.1.

## Why nothing here yet?

v0.1 is a fresh extraction from a single-operator system. Shipping a
"worked example" before the protocol has been dogfooded outside that
system would be premature — the example would just be a slice of the
extraction's home environment.

The first real example will land at v0.2, after the protocol has been
applied to a different domain than the one it grew out of.

## What an example would look like

Each example here will eventually be a full atomic-lab — the eight
dirs, the three top-level docs, a few real `events.log` entries, and
a `README.md` per example explaining:

- What concern the lab is for
- What domain-specific events (if any) it added
- What survived from the protocol untouched
- What broke and why

If you build an atomic-lab that fits some interesting shape and want
to contribute it as an example, file an issue with a one-line headline
and a link to your repo. After v0.2, examples may be vendored in.

## Until then

Read [`../docs/getting-started.md`](../docs/getting-started.md) and
build your own. The protocol's strongest signal will come from labs
that exist in the wild, not from canonical examples in this repo.
