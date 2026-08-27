---
name: write-intent
description: Turn a framed, evidence-checked opportunity into a short, approvable product intent doc that states direction and rationale before scope or spec work begins. Use when an opportunity has come out of `opportunity-framing` or `problem-validation` and is ready to move from "should we" to "here's the direction," when a stakeholder wants a one-page "why are we doing this, and why now" doc before engineering scoping starts, or right before `write-feature-spec` so the spec can inherit an already-approved rationale instead of re-deriving one mid-spec.
argument-hint: "<opportunity statement, plus evidence and known constraints -- or an opportunity-framing/problem-validation output>"
---

<!-- sourcing: drafted-fresh -->

# Write Intent

Turn a validated opportunity into a short intent doc a human can approve — direction and rationale, not scope or implementation detail.

## Usage

```
/write-intent $ARGUMENTS
```

## Competency Connection

This skill is the practical exercise of two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Product Strategy > Product Vision & Roadmapping** — the model defines this as connecting a product area to team and company strategy, not just shipping a good feature. The "Why This / Why Now" and "Success Looks Like" sections are exactly that connective work done on paper: they force an explicit link from a single initiative back to why it matters now, which is the artifact a leader can point to as evidence of roadmapping judgment rather than just feature output.
- **Product Execution > Feature Specification** — the model frames good specs as rallying a team around a goal with enough detail to execute against, not as re-litigating "why are we doing this" mid-document. By producing the rationale, non-goals, and constraints a spec should already have settled, this skill keeps `write-feature-spec` focused on behavior and scope instead of re-deriving direction — which is what keeps a spec's Feature Specification evidence about execution clarity, not strategy debate.

## Required Inputs

- The opportunity statement itself (ideally an `opportunity-framing` output, a `problem-validation` recommendation, or an equivalent restated claim about who is affected and what problem exists)
- Evidence behind the opportunity (carried over from `opportunity-framing`'s Evidence section or `problem-validation`'s Current Evidence Strength, if it went through either — otherwise stated directly)
- Who is affected (the segment or user type the opportunity names)
- Any known constraints (technical, resourcing, timeline, organizational, or "none known yet")

## If Inputs Are Missing

- **The opportunity hasn't gone through `opportunity-framing` or `problem-validation`**: do not draft "Why This / Why Now" from assumption. Ask for at least the evidence and who-is-affected information before drafting that section — a bare opportunity description without those two things behind it is not enough to write a rationale, only enough to ask for one.
- **Evidence is present but thin or unsourced**: proceed, but say so plainly in "Why This / Why Now" rather than writing the rationale as if the evidence were stronger than it is.
- **No known constraints stated**: do not invent plausible-sounding ones. Write "No constraints known yet" in that section and flag it as a gap the approver should close before commitment, rather than a solved question.
- **Success criteria are vague or unmeasurable** ("users will love it," "this will improve engagement"): do not accept the language as written. See Constraints below — this is this skill's core discipline, not an edge case.

## Process

1. **Restate the opportunity** in one or two sentences, as given — no editorializing yet.
2. **Check what's behind it.** Confirm evidence and affected-user information exist, either carried over from `opportunity-framing` / `problem-validation` or stated directly in this run's input. If neither is present, stop and ask for them before continuing to step 4 (see If Inputs Are Missing).
3. **Draft the Intent Statement.** One paragraph: what this is, for whom, and the shape of the direction being proposed — not a solution spec, not a list of features.
4. **Write Why This / Why Now**, citing the evidence and affected-user information directly rather than restating enthusiasm for the idea. If evidence is thin, say so here rather than smoothing over it.
5. **Draft Success Looks Like, qualitatively.** Describe the change a user or the business would visibly experience if this succeeds — deliberately before metrics exist. If the input's success language is vague or unmeasurable, push back on it explicitly (see Constraints) rather than transcribing it, and rewrite it as a concrete, qualitative, observable statement.
6. **List Explicit Non-Goals.** Decisions already made about what this intent does NOT cover — settled now, not deferred.
7. **List Known Constraints.** Technical, resourcing, timeline, or organizational limits already known, stated as given (never invented — see If Inputs Are Missing).
8. **List Open Strategic Questions**, kept genuinely distinct from step 6. A non-goal is a decision already made; an open strategic question is something unresolved that more information could still answer (budget not yet confirmed, a dependent team's roadmap not yet set, a build-vs-buy call not yet made). Do not let an unresolved-but-answerable question hide in Non-Goals, and do not let a settled scope boundary hide in Open Questions.
9. **Name who needs to approve** this intent before it can be treated as a legitimate input to spec work — by role, not a generic "leadership."

## Constraints

- **No upstream evidence, no fabricated rationale.** If the opportunity hasn't been through `opportunity-framing` or `problem-validation`, this skill must ask for at least the evidence and affected-user information rather than inventing a plausible-sounding "Why This / Why Now." This is the repo's evidence-thin rule applied to this skill.
- **Never accept vague or unmeasurable success language as written.** "Users will love it," "this will improve engagement," or any Success Looks Like statement with no observable, describable change must be pushed back on and rewritten into something concrete and qualitative before the doc is considered complete — even though this section is deliberately pre-metrics, "pre-metrics" is not the same as "unfalsifiable."
- **Explicit Non-Goals and Open Strategic Questions must stay genuinely separate sections.** A decision already made (non-goal) is not the same thing as a question still open (strategic question). Conflating the two either hides an unmade decision as if it were settled, or dresses up a real scope boundary as something still up for debate.
- **Do not invent constraints, sizing, or approval names to make the doc look more complete.** State "not known yet" explicitly wherever information is genuinely missing, and flag it as a gap for the approver to close.
- **This skill produces a draft for approval, not a decision.** It must never present its own output as already approved, and the Approval Needed From section is mandatory, not optional.

## Output Format

```
# Intent: [short name]

## Intent Statement
[One paragraph: what this is, for whom, and the shape of the proposed
direction]

## Why This / Why Now
[Cites evidence and affected-user info directly; states plainly if evidence
is thin rather than smoothing it over]

## Success Looks Like
[Qualitative, pre-metrics -- a concrete, observable change, not a vague
aspiration. If the input's success language was vague, note what it was
rewritten from and why.]

## Explicit Non-Goals
- [Decision already made about what this does NOT cover]
(repeat)

## Known Constraints
[Technical, resourcing, timeline, organizational -- or "none known yet"]

## Open Strategic Questions
- [Something genuinely unresolved that more information could answer --
  distinct from a non-goal]
(repeat)

## Approval Needed From
[Named role(s) -- who must approve this before it's a legitimate input to
write-feature-spec or scoping work]
```

## Review Checkpoints

- A human must confirm the evidence and affected-user information behind "Why This / Why Now" are accurately represented — especially if this intent skipped `opportunity-framing` or `problem-validation` and was asked for directly.
- A human must approve the rewritten "Success Looks Like" statement — confirm the qualitative rewrite still means what the original stakeholder intended, not just that it sounds more measurable.
- The named approver(s) in "Approval Needed From" must actually sign off before this doc is treated as a legitimate input to `write-feature-spec` or any scoping conversation. This skill drafts an intent doc for a human to approve — it does not decide whether the direction is right.

## Common Mistakes

- **Accepting vague success language at face value.** "Users will love it" gets written into the doc unchanged instead of being challenged and rewritten into something concrete enough that someone could later say whether it happened.
- **Conflating non-goals with open questions.** Writing "pricing model" into Non-Goals when it's actually undecided, or writing a genuinely settled scope boundary into Open Strategic Questions to soften it — both blur a distinction the doc exists to make clear.
- **Fabricating "Why This / Why Now" when the opportunity never went through evidence-checking.** Skipping the check in Process step 2 and writing a confident rationale anyway is the single most damaging failure mode this skill exists to prevent.
- **Treating the intent doc as the spec.** Wandering into user flows, edge cases, or acceptance criteria — that's `write-feature-spec`'s job, once this doc is approved.

## Practice Questions

- If a skeptical engineer read only "Success Looks Like," could they picture roughly what would be different for a user — or is it still just a feeling?
- Could every item in "Explicit Non-Goals" be defended as a decision already made today, and every item in "Open Strategic Questions" be defended as something more information could still resolve?
- Does "Why This / Why Now" point at evidence classified somewhere else (this run's input, or an `opportunity-framing` / `problem-validation` output), or is it restating enthusiasm for the idea?

## Improvement Loop

After an intent doc is approved (or sent back), track what happened: did the rewritten "Success Looks Like" statement survive contact with real metrics once a spec defined them, did any "Non-Goal" get silently reopened during spec work, did an "Open Strategic Question" ever actually get answered or just get ignored until it caused rework. Feed that back into how strictly this skill pushes back on vague success language and how it distinguishes non-goals from open questions next time — that is what keeps "Product Vision & Roadmapping" evidence honest instead of aspirational.
