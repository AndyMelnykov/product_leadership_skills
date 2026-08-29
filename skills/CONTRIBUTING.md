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
     sourcing-transparency and "nothing invented" rules for this section.
     In the meantime, five skills added in Block F (opportunity-framing, problem-validation,
     write-intent, define-success-metrics, identify-product-risks) had to author their own
     Review Checkpoints "what a human must approve" language against this placeholder --
     re-audit those five against the real Agent-can-do / Human-should-own lists once this
     section is filled in, rather than assuming they were already reconciled (see plan Task 33
     quality-bar self-audit). write-decision-brief (Block G) hit the same placeholder and is
     flagged for the same re-audit. compare-options (Block G) hit the same placeholder and
     is flagged for the same re-audit. -->

**Agent can do:**

- TODO — reproduce verbatim from `docs/vision/product-leadership-skills-vision.md`'s "Human judgment boundaries" section once filled in.

**Human should own:**

- TODO — reproduce verbatim from `docs/vision/product-leadership-skills-vision.md`'s "Human judgment boundaries" section once filled in.

Every skill's `Review Checkpoints` section should draw its "what a human must approve" language from this list, not invent its own boundary.

## Sourcing a new skill

Before hand-authoring any new skill, search for an existing, freely reusable example first — only draft from scratch if nothing suitable is found. This procedure is defined once here and applies to every new skill in this repo.

1. **Search first.** For the skill's stated purpose, search: (a) Anthropic's official Claude skill examples (anthropic-cookbook / anthropic-quickstarts / any published Claude "Agent Skills" example repos), (b) community lists such as "awesome-claude-skills" / "awesome-claude-code" on GitHub, (c) general GitHub/web search for `"<skill purpose>" claude skill` or `"<skill purpose>" prompt template product management`. Use WebSearch/WebFetch for this — do not rely on memory of what might exist.
2. **Evaluate candidates against this repo's bar**, not against how polished they look: does the candidate specify inputs, missing-input behavior, constraints, and output structure? Does it avoid turning weak evidence into strong claims? Most generic prompt-library hits will fail this bar — that's expected and is itself useful signal that hand-authoring is warranted.
3. **If a usable candidate exists:** adapt it — rewrite to this repo's SKILL.md contract and frontmatter shape, add the competency connection, add constraints/missing-input-behavior if the source lacked them, and record `<!-- sourcing: adapted-from-<url> -->` at the top of the file.
4. **If nothing suitable is found:** draft from scratch using [`_TEMPLATE/SKILL.md`](_TEMPLATE/SKILL.md), using `synthesize-research` or `prep-competency-review` as style references (they are the most complete existing skills), and record `<!-- sourcing: drafted-fresh -->`.
5. **Either way:** the skill still needs its own `evals/` (at least 1 case, 2+ preferred) before the task is done — sourcing an example does not exempt a skill from evaluation.
