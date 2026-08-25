# Contributing a Skill

This guide covers the anatomy of a skill in this repo, the rules every skill's `Process` section must respect when it draws on more than one source of context, and how to source a new skill before hand-authoring one from scratch.

Start new skills from [`_TEMPLATE/SKILL.md`](_TEMPLATE/SKILL.md) — it maps 1:1 to the 9-part skill contract (Purpose, Trigger, Inputs, Missing input behavior, Process, Constraints, Output, Review, Evaluation) that every skill in this repo must be traceable to, per the repo's Global Constraints.

## Skill anatomy

Every skill needs a `SKILL.md`. Not every skill needs anything else.

- **`SKILL.md` only** — the default. Most skills' full guidance fits in the file itself; keep it that way unless one of the reasons below applies.
- **`references/`** — add only when a skill leans on a durable framework or methodology doc substantial enough that inlining it would bury the skill's own Process/Constraints sections (for example, a scoring rubric or a multi-page checklist reused across several Process steps). A single paragraph of background does not justify a references file.
- **`examples/`** — add only for a flagship skill getting golden examples (a `strong-example.md` and `weak-example.md` pair), and only once real example content exists. An empty or aspirational `examples/` folder is worse than none.
- **`evals/`** — add once the skill has at least one real eval case in the `skill/case/expected` shape (see below). Every skill should eventually have this; a skill without it yet just doesn't have the folder.

**Do not create empty `references/`, `examples/`, or `evals/` folders "for completeness."** A subfolder is added by the task that populates it with real content, never in advance of that content.

## Source hierarchy

When a skill's `Process` cites more than one kind of input, resolve conflicts between them using this order, highest authority first:

1. Approved decision
2. Canonical docs
3. Current customer evidence
4. Meeting notes
5. Working drafts
6. Agent inference

A skill whose Process draws on multiple sources should say so explicitly — state which source wins when two disagree, using this ordering, rather than silently picking one or averaging them.

## Context rules

A skill states the *minimum* context it needs to do its job. Never instruct a skill (or a subagent executing one) to "read everything" in a folder, repo, or research pile before it can proceed. If a skill's `Required Inputs` section can't be stated as a specific, bounded list, that's a sign the skill's scope is too broad.

## Human judgment boundaries

<!-- STATUS: pending. docs/vision/product-leadership-skills-vision.md is currently a placeholder
     skeleton (its own "Human judgment boundaries" section is a TODO) because the source
     05-product-leadership-skills.md doc was not available when Block A was implemented. The
     Agent-can-do / Human-should-own lists below must be filled in verbatim from that section
     once the vision doc has real content -- do not draft these from scratch, per the repo's
     sourcing-transparency and "nothing invented" rules for this section. -->

**Agent can do:**

- TODO — reproduce verbatim from `docs/vision/product-leadership-skills-vision.md`'s "Human judgment boundaries" section once filled in.

**Human should own:**

- TODO — reproduce verbatim from `docs/vision/product-leadership-skills-vision.md`'s "Human judgment boundaries" section once filled in.

Every skill's `Review Checkpoints` section should draw its "what a human must approve" language from this list, not invent its own boundary.

## Sourcing a new skill

Before hand-authoring any new skill, search for an existing, freely reusable example first — only draft from scratch if nothing suitable is found. The full search-first procedure (where to search, how to evaluate candidates against this repo's bar, and the `adapted-from-<url>` / `drafted-fresh` sourcing note) is defined once in Block E of the expansion plan and applies to every skill in Blocks F-J. See `docs/superpowers/plans/2026-08-23-product-leadership-skills-expansion.md` Task 11 (this section will be filled in here directly once that task runs, per the plan's own instruction to append it to this file).
