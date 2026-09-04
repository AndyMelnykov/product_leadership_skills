---
name: agent-readiness-review
description: Assess whether a described product workflow is actually suitable for handoff to an autonomous agent, before any automation is built -- surfacing reversibility of the agent's actions, the cost of a failure, and the human checkpoints the workflow needs. Use before automating a workflow with an agent, when someone proposes "let's have an agent do X," or when reviewing an existing agent handoff for gaps in oversight.
argument-hint: "<the workflow description you want to hand to an agent, plus what happens if the agent gets it wrong>"
---

<!-- sourcing: drafted-fresh -->
<!-- Search performed per CONTRIBUTING.md "Sourcing a new skill": WebSearch turned up several
     "agent readiness" Claude skills (netresearch/enterprise-readiness-skill,
     viktor-silakov/readiness, mcpmarket's "AI Agent Readiness Report" and "Readiness Report"),
     but all of them score a *codebase/repository's* readiness for an agent to work in it
     (linting, tests, CI/CD, docs, CODEOWNERS, maturity level 1-5) -- a different subject
     entirely from this skill's job, which is judging whether a *described product workflow*
     is safe to hand to an agent at all. None of them assess reversibility of the agent's
     actions or the cost of a wrong action, and none treat an unstated reversibility/cost as a
     blocking finding rather than a low-risk default -- confirmed directly against
     viktor-silakov/readiness's own docs. Anthropic's "Building Effective Agents" guidance
     (error-cost and human-checkpoint framing) is a relevant conceptual reference but is not
     itself a skill artifact with inputs/missing-input-behavior/constraints/output structure to
     adapt from. Nothing found meets this repo's bar, so this skill is drafted fresh. -->

# Agent Readiness Review

Assess whether a described workflow is actually safe to automate with an agent, before it is built or handed off.

## Usage

```
/agent-readiness-review $ARGUMENTS
```

## Competency Connection

This skill exercises two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Strategic Impact** (under **Product Strategy**) -- the model defines this as understanding and contributing to business strategy and bringing it to fruition through *consistent delivery of business outcomes*, not through activity. Deciding whether a workflow is genuinely ready for autonomous agent handoff -- rather than automating it because agents are available -- is a strategic call about where automation actually pays off versus where it introduces risk the business hasn't priced in. A PM who defaults every "can an agent do this" question to "sure, try it" is optimizing for activity, not outcomes.
- **Product Quality** (under **Product Execution**) -- the model notes that quality issues rarely move metrics in an obviously attributable way, which is exactly why they get deprioritized, yet they erode trust until a competitor arrives. An agent workflow that fails silently, takes an irreversible action, or has no human checkpoint is a quality failure waiting to happen. Running this review and producing a specific, checkpoint-anchored verdict is the evidence that quality was actually assessed before automation shipped, not assumed.

## Required Inputs

- **The workflow description**: what the agent would actually do, step by step -- which systems it touches, what triggers it, and what its actions are (e.g. "reads support tickets, drafts a refund, issues it via the billing API" is a workflow; "handle refunds" is not).
- **The cost of the agent getting it wrong**: what happens if the agent's output or action is simply incorrect -- financial cost, customer-facing damage, compliance exposure, or internal cleanup effort. A number or an order of magnitude is useful but not required; a concrete description of the worst plausible outcome is the minimum.
- **The reversibility of the agent's actions**: can a wrong action be undone -- fully, partially, or not at all -- and if so, how (a rollback, a manual correction, a refund-the-refund) and at what cost/delay to reverse it.

## If Inputs Are Missing

- **Workflow description is vague or scoped as an outcome rather than steps** (e.g. "have an agent manage renewals"): ask for the actual sequence of actions and systems touched before proceeding. A review of an outcome instead of a workflow can't identify where the agent's actions actually land.
- **Reversibility or failure cost is unstated**: do not proceed to a verdict, and do not assume low risk as the default. Per the Constraints below, treat the absence itself as a blocking unknown -- report it explicitly as the reason a "ready" or "ready-with-guardrails" verdict cannot be issued yet, and ask the requester to state it (or state that it is genuinely unknown, which is itself informative and still blocks a ready verdict).
- **Required human checkpoints are unstated**: this is not something to ask about upfront -- propose candidate checkpoints as part of the review's own output (see Process step 4), since identifying where a human should intervene is part of this skill's job, not a precondition for doing it.

## Process

1. Restate the workflow as a concrete sequence of agent actions and the systems/data each action touches. If the description given is really a goal or outcome rather than a sequence of actions, stop and ask for the actual steps (see If Inputs Are Missing) rather than inferring a plausible-sounding sequence.
2. Determine reversibility for each action in the sequence that changes state (sends something, spends something, deletes something, commits something) -- not just the workflow as a whole. Classify each as fully reversible, partially reversible (with cost/delay to undo), or irreversible. If the requester hasn't stated this, do not infer it from the action's apparent nature (e.g. do not assume "sending an email" is low-stakes) -- flag it as unstated per Constraints.
3. Determine the failure cost for the workflow: what a wrong output or action actually costs if it goes uncaught -- in money, customer trust, compliance exposure, or cleanup labor. Distinguish cost-if-caught-immediately from cost-if-it-runs-unattended for a while, since agents that run on a schedule or in a loop can compound a single bad decision.
4. Identify candidate human checkpoints: points in the sequence where a human should review or approve before the agent proceeds, based on where reversibility drops or failure cost rises in steps 2-3. Prefer checkpoints before the first irreversible or high-cost action, not after.
5. Cross-check reversibility and failure cost against each other: a highly reversible action with high failure cost (e.g. an easily-undone but reputationally damaging public post) and an irreversible action with low failure cost (e.g. a one-time internal log entry) call for different guardrails -- do not treat "irreversible" and "high-cost" as the same finding.
6. Determine the readiness verdict using the rule in Constraints: if reversibility or failure cost was unstated and never resolved during this review, the verdict cannot be "ready" or "ready-with-guardrails" -- it is "not-ready" pending that information, regardless of how well-specified the rest of the workflow is.
7. If the verdict is "ready-with-guardrails" or "not-ready," specify the guardrails needed to move toward "ready": specific checkpoints, scope limits, dry-run/shadow periods, or additional monitoring -- not a general "add more oversight."
8. Compile findings into the Output Format below.

## Constraints

- **Unstated reversibility or failure cost is a blocking unknown, not a low-risk default.** This skill must never assume an unstated action is reversible, or an unstated failure is cheap, in order to produce a clean "ready" verdict. When either is unstated and not resolved during the review, the verdict is "not-ready," and the output must say plainly that this is why.
- **Never let a well-written workflow description substitute for actual risk information.** A workflow can be described in exhaustive, confident detail and still be missing the two facts (reversibility, failure cost) that determine whether it should be automated -- clarity of description is not evidence of safety.
- **Do not average or net out risk across steps.** A workflow with nine fully-reversible steps and one irreversible, high-cost step is governed by that one step, not by the average of the ten.
- **A "ready" verdict is not a promise of correctness.** It means the workflow's risk profile is understood and acceptable with normal monitoring -- it does not mean the agent will perform the task well, which this skill cannot evaluate without seeing actual runs.

## Output Format

```
# Agent Readiness Review: [Workflow Name] -- [Date]

## Workflow Summary
[The concrete sequence of agent actions and systems touched, as restated in Process step 1.]

## Reversibility of Actions
- [Action]: fully reversible / partially reversible (cost/delay to undo: ...) / irreversible / UNSTATED -- blocking
- ...

## Failure Cost If Wrong
[What a wrong output or action costs, distinguishing caught-immediately vs. runs-unattended. State "UNSTATED -- blocking" if the requester did not provide this and it wasn't resolved during the review.]

## Required Human Checkpoints
- Before [action]: [why -- reversibility drop, cost rise, or both]
- ...

## Readiness Verdict
ready / ready-with-guardrails / not-ready
[One or two sentences on why, explicitly naming the deciding factor -- especially if the verdict is "not-ready" because reversibility or failure cost was unstated.]

## Guardrails Needed If Not Fully Ready
[Specific checkpoints, scope limits, dry-run periods, or monitoring needed to move toward "ready." State "N/A -- verdict is ready" if not applicable.]
```

## Review Checkpoints

- **A human who owns the workflow's business risk must approve the readiness verdict before any build or handoff proceeds** -- this review informs the decision; it does not make it.
- **A human should confirm the stated failure cost and reversibility are actually accurate**, not just present -- this skill can only assess what it's told; it cannot independently verify that a "reversible" action really is, or that a stated cost estimate is realistic.
- **Someone with authority over the target systems should confirm the proposed human checkpoints are enforceable** -- a checkpoint this review recommends is only as good as the mechanism (an approval gate, a review queue) that actually pauses the agent there.

## Common Mistakes

- **Treating "the workflow is well-documented" as evidence it's safe to automate.** A precise, confident description of the steps says nothing about what happens when the agent gets one of them wrong.
- **Defaulting an unstated reversibility or cost to "probably fine" to avoid blocking the request.** This is the exact failure this skill exists to prevent -- silence on either input must read as "not-ready," not as permission to proceed.
- **Assessing reversibility for "the workflow" as a whole instead of per action.** A workflow with one irreversible step buried in the middle looks safe if reversibility is only judged at the workflow level.
- **Recommending generic oversight ("have someone check the output periodically") instead of a specific checkpoint tied to where reversibility drops or cost rises.**
- **Confusing "ready" with "will perform the task correctly."** This review assesses whether the risk is understood and bounded, not whether the agent is actually good at the task.

## Practice Questions

- For every state-changing action in this workflow, can I point to exactly how it would be undone if the agent got it wrong -- or did I leave that unstated and move on anyway?
- If the failure cost turns out to be an order of magnitude higher than assumed, does the recommended verdict and guardrail set still hold?
- Did any checkpoint I proposed get placed after the first irreversible or high-cost action instead of before it?

## Improvement Loop

After a workflow goes live following a "ready" or "ready-with-guardrails" verdict, track whether any incident occurred at a step this review classified as reversible or low-cost -- a miss there means the classification method (not just this one review) needs tightening. Also track how often "not-ready" verdicts caused by unstated reversibility/cost were later resolved with information that was knowable all along (a sign requesters need to be asked earlier) versus genuinely novel risk uncovered only during this review (a sign the review process is earning its keep).
