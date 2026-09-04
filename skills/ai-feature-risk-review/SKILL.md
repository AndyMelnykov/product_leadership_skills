---
name: ai-feature-risk-review
description: Review an AI-powered feature before it ships for user harm, incorrect-action risk, data exposure, permission boundaries, and failure recovery -- with an unstated autonomy boundary (what the AI can do without human approval) always surfacing as the top finding rather than being assumed safe. Use before shipping an AI-powered feature, when a feature description mentions a model taking actions or making decisions, or when reviewing an existing AI feature after an incident or before expanding its scope.
argument-hint: "<the AI feature description, what it can do autonomously vs. with approval, and what data it can access>"
---

<!-- sourcing: drafted-fresh -->
<!-- Search performed per CONTRIBUTING.md "Sourcing a new skill": WebSearch for Anthropic-published
     skill examples, "awesome-claude-skills" lists, and general checklists turned up several
     candidates -- generic "responsible AI" / "AI product launch" checklists (WeAreDevelopers,
     Lumenalta, TrustArc, ProductSchool), governance-framework skills (an NIST AI RMF skill, an
     ISO 42001 AI Governance skill, Sushegaad/Claude-Skills-Governance-Risk-and-Compliance), and
     Anthropic's own Responsible Scaling Policy. None of these are skill artifacts with this
     repo's contract (specific required inputs, missing-input behavior, constraints, output
     structure) to adapt from -- the governance-framework skills operate at NIST/ISO/EU-AI-Act
     control-catalog granularity, not at the level of a single feature's ship decision, and a
     direct check (via WebFetch against Sushegaad/Claude-Skills-Governance-Risk-and-Compliance)
     confirmed none of them treat an undefined autonomy/permission boundary as a blocking,
     surfaced-first finding -- they cover human oversight as one control among many, not as a
     rule that overrides a clean rating. Anthropic's Responsible Scaling Policy is a relevant
     conceptual reference (pre-deployment testing, capability-scaled safeguards) but operates at
     frontier-model-launch granularity, not single-feature-ship granularity, and is not itself a
     skill artifact to adapt. Nothing found meets this repo's bar, so this skill is drafted
     fresh, following the same discipline used in this repo's agent-readiness-review skill
     (unstated reversibility/cost blocks a "ready" verdict) applied to a different set of risk
     categories. -->

# AI Feature Risk Review

Review an AI-powered feature before it ships for the five risk categories named in the vision doc, with an unstated autonomy boundary always surfacing first.

## Usage

```
/ai-feature-risk-review $ARGUMENTS
```

## Competency Connection

This skill exercises two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Product Quality** (under **Product Execution**) -- the model notes that quality issues rarely move metrics in an obviously attributable way, which is exactly why they get deprioritized, yet poor quality slowly erodes trust and loyalty until a competitor arrives. An AI feature that harms a user, acts on a wrong inference, leaks data it shouldn't have touched, or fails silently is a quality failure with an unusually high blast radius. Running this review and producing a specific, category-by-category finding set before shipping is the evidence that quality was actually assessed, not assumed because "the model seemed to work in testing."
- **Strategic Impact** (under **Product Strategy**) -- the model defines this as understanding and contributing to business strategy and bringing it to fruition through consistent delivery of business outcomes, not through activity. Shipping an AI feature with an unbounded or unexamined autonomy boundary is a strategic exposure, not just a technical one: one bad autonomous action can undo the trust that months of "AI feature velocity" built. A PM who treats "ship the AI feature" as the outcome, rather than "ship an AI feature whose risk is understood and bounded," is optimizing for activity over the business outcome the model calls for.

## Required Inputs

- **The feature description**: what the AI-powered feature actually does -- the task it performs, the trigger that invokes it, and the surface it's exposed on (a chat reply, an automated action, a recommendation shown to a user).
- **The autonomy boundary**: exactly what actions the AI can take without human approval, versus what requires a human to review or approve first. This is the single most load-bearing input this skill uses (see If Inputs Are Missing and Constraints).
- **The data it can access**: what data sources, systems, or user information the feature reads or can act on, including anything it can access indirectly through tool calls, retrieved context, or logs.

## If Inputs Are Missing

- **The autonomy boundary is not specified**: do not ask-and-wait, and do not assume it is narrow or safe by default. Per the Constraints below, treat this absence itself as the top risk finding of the review, state it first in the output (see Output Format), and proceed through the rest of the review under the presumed-worst-case boundary (fully autonomous, no approval gate) until the requester resolves it. Every other section's findings are conditioned on this presumption and must say so.
- **The feature description is vague or stated as a goal rather than a concrete behavior** (e.g. "use AI to help with support" instead of "an AI drafts and sends a reply to support tickets classified as low-complexity"): ask for the concrete behavior before proceeding. A review of a goal instead of a described behavior can't locate where harm, incorrect actions, or data exposure would actually occur.
- **Data access is unstated**: do not assume the feature only touches the data explicitly mentioned in the feature description. Ask what it can access, and if the requester doesn't know or hasn't checked (e.g. because retrieved context or a tool call could pull in more than intended), flag that as an open item under Data Exposure rather than silently scoping the review to only what was described.

## Process

1. Restate the feature description as a concrete behavior: what it does, what triggers it, and what surface it's exposed on. If it's stated as a goal rather than a behavior, stop and ask (see If Inputs Are Missing).
2. Determine the autonomy boundary status first, before any other analysis: is it explicitly stated (what the AI can do without approval vs. with approval), or unstated? If unstated, this is the review's top finding -- record it now so it can be placed first in the output, and proceed through steps 3-7 under the presumed-worst-case boundary (fully autonomous) rather than waiting for an answer.
3. Identify user harm scenarios: concrete ways a real user could be harmed by this feature -- financially, emotionally, reputationally, physically, or through a degraded/blocked experience. Ground each scenario in the actual feature behavior from step 1, not a generic AI-risk template.
4. Assess incorrect-action risk: for each thing the AI decides or does, what happens specifically when the model is simply wrong -- a wrong classification, a hallucinated fact, a bad recommendation, a wrong action taken. Distinguish a wrong output that a human still reviews from a wrong action the AI executes itself, since the second is gated entirely by the autonomy boundary from step 2.
5. Assess data exposure: what data the feature can read or touch (per Required Inputs), whether it can be exposed to the wrong user (cross-tenant leakage, a reply shown to the wrong person), retained somewhere unintended (logs, training data, a third-party model call), or inferred beyond what was explicitly shared.
6. Assess permission boundaries in full: expand on the autonomy-boundary finding from step 2 into a complete accounting of what the AI can do unilaterally versus what requires approval, action by action if the feature does more than one thing. If the boundary was unstated, this section restates that finding rather than introducing a new, softer framing of it.
7. Assess failure recovery: what happens when the feature fails -- the model errors out, times out, or the surrounding system it calls fails. Does the feature fail safe (blocks, defers to a human, does nothing) or fail open (proceeds with a default, retries blindly, takes the action anyway)? State which, and what a user or operator experiences either way.
8. Determine the overall risk rating using the rule in Constraints: an unstated (and unresolved) autonomy boundary caps the rating at High or Critical regardless of how contained the other four categories look. Where the boundary is stated, weigh the rating on the worst single finding across all five categories, not their average.
9. Compile findings into the Output Format below, with the autonomy-boundary check as the first thing a reader sees.

## Constraints

- **An unstated autonomy boundary is the top risk finding, not a gap to note in passing.** It must appear first in the output, ahead of User Harm Scenarios, and it must never be silently treated as "probably narrow" or "probably requires approval" in order to produce a clean review.
- **Never assume an unstated boundary is safe because the feature description sounds contained.** A feature described in careful, specific detail can still omit the one fact (what it can do without a human in the loop) that determines whether it's shippable.
- **Do not average risk across the five categories.** A feature that is low-risk on user harm, data exposure, and failure recovery but has an unstated or unbounded autonomy boundary is governed by that one finding, not by the average of five.
- **Do not let a passing eval or a clean test run substitute for this review.** This review assesses risk categories a functional test does not cover (harm, exposure, permission scope, failure mode) -- "it worked in testing" is not evidence against any of the five findings.
- **A "Low" or "Medium" overall risk rating is never available while the autonomy boundary is unstated and unresolved**, per Process step 8 -- state this plainly if it's the reason the rating is capped higher than the other findings alone would suggest.

## Output Format

```
# AI Feature Risk Review: [Feature Name] -- [Date]

## TOP FINDING: Autonomy Boundary
[State the boundary as given: what the AI can do without approval vs. with approval.
If UNSTATED: "UNSTATED -- this is the top risk finding of this review. Every finding
below is assessed under the presumed-worst-case boundary (fully autonomous, no approval
gate) until this is resolved." This section always appears first, regardless of how
severe or mild the other five sections turn out to be.]

## User Harm Scenarios
- [Scenario]: [who is harmed, how, and how severely]
- ...

## Incorrect-Action Risk (If the Model Is Wrong)
- [Decision/action]: [what happens if the model gets this wrong] -- reviewed by a human
  before it takes effect / executed autonomously (see Autonomy Boundary above)
- ...

## Data Exposure
- [Data touched]: [exposure risk -- wrong-recipient leakage, unintended retention, or
  inference beyond what was shared]
- ...

## Permission Boundaries
[Full accounting of what the AI can do unilaterally vs. what requires approval, action
by action. If the top-level boundary was unstated, restate that here rather than
introducing a softer framing.]

## Failure Recovery
[What happens when the feature fails: fails safe (blocks/defers/no-ops) or fails open
(proceeds with a default, retries, acts anyway) -- and what a user or operator
experiences either way.]

## Overall Risk Rating
Rating: Low / Medium / High / Critical
Rationale: [Name the deciding factor explicitly. If capped by an unstated autonomy
boundary, say so plainly rather than blending it into a general summary.]
```

## Review Checkpoints

- **A human who owns the feature's business and safety risk must approve the risk rating and any ship decision** -- this review informs that decision; it does not make it.
- **A human must resolve the autonomy boundary before the feature ships**, if it was unstated at review time -- this review cannot substitute a presumed-worst-case boundary for a real, deliberate one; it only prevents that gap from being shipped unnoticed.
- **A human familiar with the feature's actual system access should confirm the stated data exposure is complete** -- this skill can only assess what it's told a feature can touch; it cannot independently discover an undisclosed tool call or retrieval path.
- **Someone with authority over the surrounding system should confirm the failure-recovery behavior described is accurate**, not assumed -- "fails safe" is a claim about system behavior, not a default to take on faith.

## Common Mistakes

- **Treating an unstated autonomy boundary as a footnote instead of the lead finding.** If it's unstated, it belongs first in the output, not folded into the Permission Boundaries section as one item among several.
- **Assuming an unstated boundary is narrow or approval-gated to avoid blocking the review.** This is the exact failure this skill exists to prevent -- silence on the boundary must read as maximum exposure, not minimum.
- **Averaging a mostly-clean review into a "Medium" rating** when one category (often permission boundaries) is actually severe -- the worst finding governs, not the mean.
- **Confusing "the model performed well in testing" with "the risk categories are addressed."** Model quality and risk containment are different questions; this review answers the second, not the first.
- **Writing generic AI-risk boilerplate for User Harm Scenarios or Data Exposure** instead of scenarios grounded in what this specific feature actually does and touches.

## Practice Questions

- Does the Autonomy Boundary section appear first in this output, and does it say "UNSTATED -- top finding" plainly if it wasn't given -- or did I bury it inside Permission Boundaries?
- If the autonomy boundary turns out to be fully autonomous (no approval gate) once clarified, does every other section's finding still hold, or did I quietly assume a human was in the loop somewhere?
- Is the overall rating driven by the single worst finding across the five categories, or did I let four clean categories dilute one severe one?

## Improvement Loop

After a feature ships following this review, track whether any incident traced back to a category this review rated as low-risk, or to an autonomy boundary that was stated but turned out not to be enforced in the actual system -- either is a signal the review method (not just this one pass) needs tightening. Also track how often an "UNSTATED -- top finding" result was resolved with information the requester had all along (a sign to ask for the autonomy boundary earlier, before the review starts) versus genuinely undecided at the org level (a sign this review is surfacing a real gap in how AI features get approved).
