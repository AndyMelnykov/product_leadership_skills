---
name: write-feature-spec
description: Turn a problem, request, or rough idea into an actionable feature specification with clear scope and measurable outcomes. Use when a PM has a feature idea, a stakeholder ask, or research findings that need to become something engineering and design can act on, or when a spec's scope and success criteria feel fuzzy.
argument-hint: "<feature idea, problem statement, or research finding to turn into a spec>"
---

# Write Feature Spec

Turn ambiguity into an actionable specification: clear scope, explicit trade-offs, and measurable outcomes.

## Usage

```
/write-feature-spec $ARGUMENTS
```

## Competency Connection

This skill exercises **Feature Specification**, one of three competencies under **Product Execution** in the [PM competency model](../../../docs/pm-competency-model.md) (see also [Product_management_execution/README.md](../../../Product_management_execution/README.md)). Product Execution is evaluated on whether a spec gives the team enough clarity to act — not on the spec's length or polish.

Use the output of this skill as competency evidence:
- A manager can review a spec's scope and success-metric sections directly against the model's "actionable specifications with measurable outcomes" bar.
- An interview rubric can ask a candidate to specify the same kind of ambiguous request this skill processes, and score it against the same checklist below — keeping hiring and review standards aligned, per the model's core principle.

## 1. Clarify the Input

Before drafting, establish:
- What triggered this? (a research finding, a stakeholder request, a metric miss, a strategic bet)
- Who is the primary user or customer this serves?
- What decision or trade-off is still open? Do not paper over it — surface it.
- Is there existing research or data to ground this in? If the input is a hunch, say so explicitly rather than presenting it as validated.

If the request traces back to user research, cross-reference relevant findings (see the `synthesize-research` skill) rather than re-deriving them from scratch.

## 2. Define Scope and Intent

- **Problem statement**: One or two sentences — what problem, for whom, why now.
- **In scope / out of scope**: Be explicit about what this spec does NOT cover. Unscoped work is the most common source of execution drift.
- **Assumptions**: List assumptions the spec depends on. If one turns out false, the spec should be revisited.
- **Dependencies**: Other teams, systems, or decisions this relies on.

## 3. Specify Behavior

- Walk through the primary user flow step by step, including edge cases and error states — not just the happy path.
- Note what happens when things go wrong (empty states, permission failures, partial data).
- Flag anything technically or organizationally risky so engineering can weigh in early rather than discovering it mid-build.

## 4. Define Success

Every spec needs a way to know if it worked:
- **Primary metric**: The one number that tells you this succeeded or failed.
- **Guardrail metrics**: What should NOT get worse as a side effect.
- **Target and timeframe**: A number and a date, not just a direction ("increase" is not a target).
- If the outcome cannot be measured, say so and propose a qualitative signal instead (e.g., support ticket themes, sales objections) — do not leave success undefined.

## 5. Sequence and De-risk

- Identify the smallest version that produces real user or business learning.
- Call out what should ship first to reduce the biggest open risk or assumption.
- Note anything that should be feature-flagged, staged, or reversible.

## Output Format

```
# [Feature Name]

## Problem
[1-2 sentences: what problem, for whom, why now]

## Goals / Non-Goals
- Goals: ...
- Non-goals (explicitly out of scope): ...

## Assumptions
- ...

## User Flow
1. ...
(include edge cases and error states)

## Success Metrics
- Primary: ...
- Guardrails: ...
- Target: ... by [date]

## Open Questions / Risks
- ...

## Rollout Plan
- ...
```

## Common Mistakes

- **Vague scope**: "Improve the settings page" is not a spec. Name the specific behavior that changes.
- **No success metric**: A spec without a measurable outcome cannot be evaluated for Product Quality later — only for whether it shipped.
- **Hidden assumptions**: An assumption not written down cannot be revisited when it turns out wrong.
- **Happy-path only**: Specs that skip error states push the ambiguity onto engineering mid-build, which is where Product Delivery timelines break.

## Practice Questions

- If an engineer read only the "Goals / Non-Goals" section, would they know what NOT to build?
- Could someone outside this project judge, from the success metrics alone, whether this shipped a good outcome?
- What is the one assumption in this spec most likely to be wrong?

## Improvement Loop

After the feature ships, revisit the spec: did the success metric move as predicted? Which assumptions held, which didn't, and which edge case was missed? Feed specific examples of scope clarity or gaps into the next performance review or coaching conversation — this is what "Feature Specification" evidence looks like in practice, not just spec volume.
