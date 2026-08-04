# AMBIGUOUS_TAGS_UPGRADE_TO_STRUCTURE_ON_SIGHT

**Org:** `RULES-OF`
**Domain:** `agent-tagging`
**Type:** Atomic rule
**Status:** Active

---

## The Rule

> Every tagging mechanism is provisional against a better one arriving.
> Encountering a worse form is a trigger to upgrade it, not just to read it.
> This applies to your own past writing and to any other agent's writing —
> including a different agent sharing your own account.

---

## Classes and objects in play

- **Tagging mechanism** — anything that marks a piece of work as belonging
  to, or requiring the attention of, a specific agent.
- **Discovery mechanism** — how an agent finds work tagged to itself. Not
  always the same system as the tagging mechanism that produced the tag.
- **Card** — a project-scoped or session-scoped agent identity, finer-grained
  than the GitHub account it operates through. Multiple cards can share one
  account; GitHub's own native features cannot distinguish between them.

## The observed state space

An audit across a real multi-org swarm (2026-08-04) found eight distinct
levels in active or dormant use, ordered roughly from least to most
structured:

1. **Bare glyph/ID mention in running prose**, no consistent prefix or
   format. Zero GitHub-native support; discoverable only by an agent's own
   ad hoc grep across bodies and comments.
2. **Shadow structured-looking prose field** (e.g. a body section that reads
   like a form field but is just markdown text: `Owner Card ID: X`). Same
   discovery cost as (1) — grep — dressed as if it were queryable.
3. **Standardized `@{card-id}` mention** — see
   `AT_PREFIX_SIGNALS_DIRECTED_ATTENTION_REGARDLESS_OF_MACHINERY` for why
   the `@` specifically matters. Still fundamentally text; still requires
   an agent's own poller to find it. Its value over (1) and (2) is
   consistency and token economy, not new structure.
4. **Real GitHub `@account` mention** — triggers the platform's own
   notification system, but resolves only to the shared account, never to
   a specific card.
5. **GitHub `assignee` / `reviewer` request** — fully native, zero
   in-body token cost, but the same account-only ceiling as (4).
6. **GitHub label** (e.g. `agent:{card-id}`) — native search
   (`gh issue list --label`), can be made card-granular by construction,
   but only if actually deployed; a repo can go a long time with this
   feature unused despite being available.
7. **Platform Project custom field** (e.g. GitHub Projects v2 fields like
   `Owner Card ID`, `Opened By Card ID`, `Awaiting Response From Card ID`)
   — queryable via the platform's structured API, card-granular by design,
   but typically exists on only one project board in an org, not
   org-wide, and the query path itself can be more fragile than a REST
   equivalent.
8. **External structured registry** (a schema'd data file or service
   decoupled from any single work item) — full schema, card-granular,
   but requires knowing to cross-reference it; it does not live on the
   GitHub object itself.

Levels (4) and (5) are a genuine ceiling, not an intermediate rung — they
cannot express card granularity no matter how much they're improved, because
the platform's own account model stops there. They pair *alongside* a
card-granular mechanism rather than being superseded by one.

## Why upgrade on sight, not just on next write

A rule that only governs what an agent writes *next* leaves every
already-written ambiguous tag exactly as ambiguous as it was, indefinitely —
the population of bad tags only shrinks if something actively rewrites the
existing ones, and nothing else in the system will do that on its own. An
agent that reads an ambiguous tag and moves on without upgrading it is
choosing to leave the next reader (possibly itself, after a compaction
boundary) to redo the same disambiguation work from scratch.

## Corollaries

- **Editing another agent's tagging, even across a shared account, is in
  scope.** Two cards operating through the same GitHub account are still
  two different agents; one correcting the other's ambiguous tag into a
  structured one is maintenance, not overreach — confirmed directly by the
  human operator of this swarm, 2026-08-04.
- **Upgrading does not mean deleting the original signal's *meaning*** —
  a level-1 mention that identified the right agent was still correct; the
  upgrade preserves who was named while improving how discoverable that
  naming is.
- **There is no single terminal state.** Levels 6, 7, and 8 do not compete —
  a label is right when the tag needs native cross-repo search; a Project
  field is right when the routing lives on one GitHub object and needs a
  board view; an external registry is right when the data is inherently
  cross-cutting (a roster, a capability map, a relationship graph) and does
  not belong to any single issue. Pick the target that matches the actual
  shape of the data, not automatically the highest-numbered level available.
- **Absence of a higher-structure mechanism in a given repo is itself a
  fact worth checking, not assuming.** A repo can go a long time looking
  like it has card-level tagging (because of consistent prose conventions)
  while actually having zero native support for it — verify the repo's
  actual labels and actual Project fields before assuming a structured
  option exists.

## Relationships (typed)

| Rule | Relationship |
|---|---|
| `AT_PREFIX_SIGNALS_DIRECTED_ATTENTION_REGARDLESS_OF_MACHINERY` | **Sibling, same domain** — explains why level 3's specific syntax is a genuine (if partial) upgrade over levels 1–2, not just a shorter string |
| `ISSUE_BODIES_CARRY_CURRENT_TRUTH_NOT_HISTORY` (`RULES-OF/github-issue-lifecycle`) | **Related discipline** — both are about not letting a written artifact stay stale once a better version of the truth (or the tag) is available |

---

*Rule formalized: 2026-08-04, extracted from a live audit of real tagging
mechanisms in use across a multi-org agent swarm — generalized here with
all project/account specifics removed.*
