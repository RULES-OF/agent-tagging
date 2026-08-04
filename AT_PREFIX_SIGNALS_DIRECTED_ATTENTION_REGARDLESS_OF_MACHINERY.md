# AT_PREFIX_SIGNALS_DIRECTED_ATTENTION_REGARDLESS_OF_MACHINERY

**Org:** `RULES-OF`
**Domain:** `agent-tagging`
**Type:** Atomic rule
**Status:** Active

---

## The Rule

> `@{name}` and `{name}` are not the same statement even when no system
> parses the `@`. One names; the other addresses.

---

## Classes and objects in play

- **Naming** — referring to an agent as a subject: "card X handled this last
  week," "card X's model tier." Informational, third-person, not directed.
- **Addressing** — referring to an agent as the intended recipient of the
  statement itself: "I am telling *you*, specifically, this." First-person
  act, directed, present-tense in intent even if read later.
- **Machinery** — whatever platform feature (if any) turns an `@`-prefixed
  token into an actual notification, link, or routing action.

## Semantics

`@` carries this meaning independent of whether any machinery acts on it.
It is not a technical trigger that happens to also read naturally to
humans — it is the natural-language marker for direct address that some
platforms *additionally* wire up to a technical trigger. The technical
wiring is a bonus when present, not the source of the meaning. This is
verified directly: on a platform where `@{card-id}` cannot resolve to any
real account (card IDs are not valid usernames — see `github-username`
constraints in `AMBIGUOUS_TAGS_UPGRADE_TO_STRUCTURE_ON_SIGHT`), the `@`
still does real semantic work for the reader, human or agent.

## Why this matters for tagging specifically

Two identically-informative strings —

```text
Owner: 🔱A♥️
@🔱A♥️
```

— are not interchangeable, even though both name the same card and both are
equally parseable by a poller script. The first states a fact about
ownership. The second is an act of address: it tells the reader "you are
who this is for," which changes how the reader should treat the surrounding
text (as a request directed at them, not as ambient status they may or may
not act on). Collapsing the two into "whichever is shorter" loses this
distinction. Prefer `@{card-id}` specifically at any point in a piece of
writing where the actual intent is "I want this agent to know I am
addressing them," and a plain naming form at any point where the intent is
purely descriptive (recording who did something, not asking anyone to do
anything).

## Corollaries

- A single comment can legitimately contain both forms: a plain name in a
  descriptive sentence, and an `@`-addressed mention in the sentence that's
  actually the ask. Don't flatten a comment to one style throughout if the
  underlying communicative acts genuinely differ line to line.
- This reasoning is platform-agnostic. It applies equally to a bare
  `{card-id}` in an internal registry record (naming) versus the same
  `card-id` written as the addressee of a message a dispatch script sends
  (addressing) — see `SKILL-OF/agent-dispatch`'s disclosure-hygiene work for
  a related distinction between what an agent is *told* versus what is
  merely *true about* it.
- Do not assume the reverse: a real, machinery-actioned `@account` mention
  is not automatically a *better* address act than a standardized
  `@{card-id}` — it is better at reaching the account, but worse (or
  incapable) at addressing the specific card. Choose based on who the
  statement is actually for, not which `@` a platform happens to route.

## Relationships (typed)

| Rule | Relationship |
|---|---|
| `AMBIGUOUS_TAGS_UPGRADE_TO_STRUCTURE_ON_SIGHT` | **Sibling, same domain** — this rule explains why that rule's level-3 standardized form is a genuine semantic upgrade, not merely a shorter string |

---

*Rule formalized: 2026-08-04, from a direct observation made mid-conversation
about why `@{card-id}` was worth adopting even though no platform machinery
reads the `@` — generalized here with all project/account specifics
removed.*
