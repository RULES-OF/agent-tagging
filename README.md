# agent-tagging

**Org:** `RULES-OF`
**Type:** Domain (aggregate) — a category of axioms, not itself an axiom
**Status:** Active

---

## What this is

Every swarm accumulates more than one way to say "this work belongs to that
agent" — GitHub-native assignment, labels, Project custom fields, free-text
mentions, external structured registries — because each was added to solve
a local problem, not designed as one coherent system. Left alone, the oldest
and least-structured forms never die; they just keep accumulating alongside
the newer, better ones.

This repo aggregates atomic rules (each still named as its own
`SCREAMING_SNAKE_CASE` proposition, one file each) about a single question:
**given more than one way exists to tag an agent to work, and more than one
way to discover that tag, what should happen when a worse form is
encountered?**

## Rules in this domain

- [`AMBIGUOUS_TAGS_UPGRADE_TO_STRUCTURE_ON_SIGHT`](./AMBIGUOUS_TAGS_UPGRADE_TO_STRUCTURE_ON_SIGHT.md)
- [`AT_PREFIX_SIGNALS_DIRECTED_ATTENTION_REGARDLESS_OF_MACHINERY`](./AT_PREFIX_SIGNALS_DIRECTED_ATTENTION_REGARDLESS_OF_MACHINERY.md)

---

*Domain formalized: 2026-08-04, extracted from a live audit of eight distinct
tagging/discovery mechanisms found in actual use (or actually absent despite
being assumed present) across the PlayFieldMultiplier/Agents-Of/SKILL-OF/
RULES-OF/OTTOPOET-00Q orgs — generalized here with all project/account
specifics removed.*
