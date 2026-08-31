# 002: Anchor every skill to the PM competency model, and fix a source hierarchy

## Context

A library of product-management prompts can grow into an unstructured pile —
useful once, un-reusable as evidence of anything. Separately, several skills
(`write-feature-spec`, `stakeholder-alignment-brief`, `prep-competency-review`)
draw on more than one kind of input (a decision already made, a canonical
doc, live customer evidence, a meeting note, a working draft) that can
disagree with each other.

## Options considered

- **No shared structure.** Each skill defines its own scope and, if it uses
  multiple sources, resolves conflicts however its author judged best at the
  time. Fastest to write, but inconsistent across skills and not reusable as
  review/coaching/hiring evidence.
- **Competency anchoring only.** Map every skill to Ravi Mehta's PM
  competency model (`docs/pm-competency-model.md`), without standardizing
  source-conflict handling.
- **Competency anchoring + a fixed source hierarchy.** Both of the above,
  applied consistently.

## Decision

Every skill states which competency/sub-competency it exercises (in prose in
its `SKILL.md`, and machine-readably in `skills/competencies.yaml`, which must
agree with the prose). Any skill whose process draws on more than one kind of
input must resolve conflicts using this fixed order, highest authority first:

1. Approved decision
2. Canonical docs
3. Current customer evidence
4. Meeting notes
5. Working drafts
6. Agent inference

## Consequences

- A skill's output can double as evidence in a performance review, coaching
  conversation, or interview calibration — the whole point of the "Product
  Leadership Skills" outcome (make repeatable product workflows executable
  *and reviewable*), not just a one-off artifact.
- New skills have a bar to clear before being added: if a proposed skill
  can't be traced to a specific sub-competency, that's a signal it doesn't
  belong in this repo (see `docs/vision/product-leadership-skills-vision.md`'s
  "avoid list" — this is not meant to become a generic prompt collection).
- The source hierarchy makes conflict resolution deterministic instead of
  silently picking whichever source the model attends to first — at the cost
  of a skill sometimes having to say a source "lost" rather than blending
  everything into one answer.
