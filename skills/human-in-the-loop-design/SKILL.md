---
name: human-in-the-loop-design
description: Classify every step of an agent-driven workflow as autonomous, reviewed, approval-required, or blocked -- with any step whose reversibility is unknown defaulting to approval-required, never autonomous. Use when designing a new agent workflow's oversight model, auditing an existing agent handoff for where human checkpoints belong, or deciding whether a step's classification can loosen after a track record of successful runs.
argument-hint: "<the workflow's steps, plus what's known about each step's reversibility and cost if wrong>"
---

<!-- sourcing: drafted-fresh -->
<!-- Search performed per CONTRIBUTING.md "Sourcing a new skill": WebSearch for Anthropic-published
     skill examples, "awesome-claude-skills" / "awesome-claude-code" lists, and general web/GitHub
     search for human-in-the-loop AI design, human oversight levels for AI agents, and autonomy
     levels for agent workflow design turned up several conceptual frameworks -- Anthropic's own
     "Building Effective Agents" (checkpoints, the autonomy/safety tradeoff), Galileo's and
     Nividous's human-oversight writeups (three-tier human-authorization / human-in-the-loop /
     human-on-the-loop models), and academic papers on task-level autonomy scales and multi-tier
     escalation. None of these is a skill artifact shaped to this repo's contract (specific
     required inputs, missing-input behavior, constraints, output structure) to adapt from -- they
     describe oversight concepts and maturity models at the level of a security operations center
     or a general agent architecture, not a step-by-step classification exercise for a described
     product workflow, and none treat an unstated/unknown reversibility as a hard floor that
     blocks a classification from ever reaching "autonomous" (several instead frame autonomy as
     something that is granted by default and revoked on risk signals -- the opposite default).
     A GitHub search for existing Claude Skills confirmed the same gap: human-in-the-loop shows up
     as a pattern embedded inside other autonomous-agent skills, not as a standalone classification
     skill. Nothing found meets this repo's bar, so this skill is drafted fresh, following the
     same discipline used in this repo's sibling skills agent-readiness-review (unstated
     reversibility/cost blocks a "ready" verdict) and ai-feature-risk-review (unstated autonomy
     boundary is the top finding) -- applied here to a step-by-step classification instead of a
     single up-or-down verdict. -->

# Human-in-the-Loop Design

Classify each step of an agent-driven workflow as autonomous, reviewed, approval-required, or blocked, so oversight is placed deliberately rather than assumed.

## Usage

```
/human-in-the-loop-design $ARGUMENTS
```

## Competency Connection

This skill exercises two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Strategic Impact** (under **Product Strategy**) -- the model defines this as understanding and contributing to business strategy and bringing it to fruition through *consistent delivery of business outcomes*, not through activity. Deciding exactly where an agent workflow needs a human checkpoint -- rather than defaulting every step to "autonomous" because that ships faster, or every step to "approval required" because that feels safe -- is a strategic call about where automation actually pays off without exposing the business to unpriced risk. A PM who can't say, step by step, why each classification is what it is has not made a strategic decision; they've made a guess.
- **Product Quality** (under **Product Execution**) -- the model notes that quality issues rarely move metrics in an obviously attributable way, which is exactly why they get deprioritized, yet poor quality slowly erodes trust until a competitor arrives. A workflow with the wrong oversight level on even one step -- an irreversible action running autonomously because nobody classified it, or a low-stakes step stuck behind a human gate that never actually adds signal -- is a quality failure in the workflow's design, not its execution. Producing a specific, per-step classification with a stated rationale is the evidence that oversight was actually designed, not left to default.

## Required Inputs

- **The workflow's steps**: the ordered, discrete actions the workflow performs -- not an outcome or goal. "Reads a support ticket, classifies it, drafts a refund, issues it via the billing API" is four steps; "handle refunds" is not a workflow.
- **The cost and reversibility of each step's actions**: for each step that changes state (sends something, spends something, deletes something, commits something), whether the action can be undone (fully, partially, or not at all) and what a wrong outcome actually costs if it goes uncaught. This can reuse the reversibility and failure-cost findings from an `agent-readiness-review` if one was already run on this workflow -- do not re-derive them from scratch if that output is available.

## If Inputs Are Missing

- **A step's reversibility is unknown or unstated**: never infer it as reversible to keep the workflow moving. Per the Constraints below, this is a hard default, not a judgment call weighed against how low the apparent cost looks: an unknown-reversibility step is classified no higher than **approval required**, and it is never classified **autonomous**, regardless of how contained the rest of the workflow appears.
- **A step's cost-if-wrong is unknown or unstated**: treat this the same way as unknown reversibility -- do not assume "probably cheap" to justify a lighter classification. An unknown cost caps the classification at approval required until the requester states it (or states plainly that it is genuinely unknown, which still caps the classification rather than defaulting to a guess).
- **The workflow is described as a goal or outcome rather than a sequence of steps** (e.g. "have an agent manage onboarding"): ask for the actual sequence of actions and systems touched before proceeding. A classification of an outcome instead of a step sequence can't say where oversight actually belongs.

## Process

1. Restate the workflow as an ordered list of discrete, state-changing steps -- each step being one action the agent takes, not a phase or a goal. If the input given is really an outcome, stop and ask for the actual sequence (see If Inputs Are Missing) rather than inferring a plausible-sounding one.
2. For each step, gather reversibility (fully reversible / partially reversible / irreversible / **unknown**) and cost-if-wrong (low / medium / high / **unknown**), reusing `agent-readiness-review` output for this workflow if it exists rather than re-deriving it.
3. Apply the hard default before anything else: any step whose reversibility is **unknown** is classified no higher than **approval required**, full stop -- this floor is applied before cost is even considered, and it cannot be argued down by a low apparent cost, a simple-looking action, or time pressure to automate. The same floor applies when cost-if-wrong is unknown.
4. For steps where reversibility and cost are both actually known, assign a classification using this decision logic, in order:
   - **Autonomous** -- fully reversible AND low cost if wrong. The agent acts without a human in the loop, before or after the fact.
   - **Review** -- fully reversible with medium/high cost, or partially reversible with low cost. The agent acts, and a human reviews the action after the fact (spot-check or full review) without blocking the workflow in real time.
   - **Approval Required** -- partially reversible with medium/high cost, or irreversible with low/medium cost, or reversibility/cost unknown (per step 3). The agent proposes the action but does not execute until a human approves it beforehand.
   - **Blocked** -- irreversible with high cost, or any step where no rollback mechanism exists at all and no approval process can meaningfully catch a bad call before it's final. The agent does not perform this step under any classification until a categorical precondition changes (a rollback path is built, a scope limit is added, a legal/compliance sign-off is obtained).
5. Classify per step, never at the workflow level -- a workflow with nine autonomous-eligible steps and one irreversible, high-cost step is governed by that one step's classification, not by an average across ten.
6. For every step landing at **Blocked**, define the escalation path: who owns unblocking it, what specifically has to happen to move it (not "get sign-off," but the actual precondition), and what the workflow does while it waits (halts entirely, routes to a manual fallback, or does not run at all).
7. For every step at **Approval Required** or stricter, define what evidence would justify loosening the classification later -- e.g., N successful, reviewed runs with no incident, or the previously-unknown reversibility being resolved to a concrete, verified answer -- and confirm that loosening moves exactly one tier at a time (Blocked to Approval Required, Approval Required to Review, Review to Autonomous), never a multi-tier jump.
8. Cross-check: does any step's classification rest on run-count or track record alone while its underlying reversibility is still marked unknown? If so, the track record does not resolve the unknown -- correct the classification back to Approval Required (or Blocked) until reversibility itself is actually established.
9. Compile findings into the Output Format below.

## Constraints

- **A step with unknown reversibility is capped at approval-required and can never be classified autonomous.** This is the one rule this skill must never trade away -- not for a low apparent cost, not for a step that "seems simple," and not because the requester is in a hurry to automate.
- **Unknown cost-if-wrong receives the same treatment as unknown reversibility.** Silence on either input must read as a ceiling on the classification, not as license to assume the low-risk case.
- **Never average or net out classification across steps.** A workflow's overall oversight design is governed by its single riskiest step, not by how many steps around it look safe.
- **A track record of successful runs cannot substitute for resolving an unknown.** N clean reviewed runs justify moving a step down one tier only if the thing that was uncertain (reversibility, cost, or both) is now actually known -- volume of runs is not itself evidence that an unknown reversibility was actually low-risk.
- **Classification can only loosen one tier at a time.** Blocked cannot jump straight to Review or Autonomous; Approval Required cannot jump straight to Autonomous. Each tier's own graduation criteria must be met in sequence.
- **"Approval required" is not satisfied by a checkpoint nobody can actually block at.** If the described approval step is a notification, a log entry, or a rubber stamp with no real ability to reject or modify the action, this skill must flag it as not actually meeting the approval-required bar rather than accept it at face value.

## Output Format

```
# Human-in-the-Loop Design: [Workflow Name] -- [Date]

## Step-by-Step Classification
| Step | Reversibility | Cost if Wrong | Classification | Rationale |
|------|---------------|---------------|-----------------|-----------|
| [step] | fully / partially / irreversible / UNKNOWN | low / medium / high / UNKNOWN | Autonomous / Review / Approval Required / Blocked | [Why -- name reversibility and cost explicitly. If reversibility or cost is UNKNOWN, the rationale must say so and confirm classification is capped at Approval Required (or Blocked) as a result, never Autonomous.] |
| ... | | | | |

## Escalation Path for Blocked Steps
- [Step]: escalation owner: [who] -- unblocked by: [the actual precondition, not "sign-off"] -- while blocked, the workflow: [halts / routes to manual fallback / does not run]
- (state "N/A -- no steps classified Blocked" if none)

## What Changes the Classification Later
- [Step]: currently [classification] -- loosens to [next tier only, one step down] after [specific graduation criteria, e.g. "N successful reviewed runs with no incident" and/or "reversibility resolved from unknown to known-[value], verified by [who/how]"]. Note explicitly if the step is still gated on an unresolved unknown -- a run count alone does not clear that gate.
- ...
```

## Review Checkpoints

- **A human who owns the workflow's business and safety risk must approve the full classification table before it governs real agent behavior** -- this skill designs the oversight model; it does not authorize it.
- **A human familiar with the actual systems involved must confirm the stated reversibility and cost figures are accurate**, not merely plausible -- this skill can only classify what it's told; it cannot independently verify that a "reversible" action truly is, or that a cost estimate is realistic.
- **The named approval-gate owner for every Approval Required step must confirm they hold real authority to reject or modify the action**, and that this is enforced by an actual mechanism (a blocking gate, not a notification) -- an approval step nobody can actually stop at is not a control.
- **Escalation owners for Blocked steps must be specific, reachable people or roles**, confirmed by someone with authority over that part of the system -- an escalation path with no real owner is not a path.

## Common Mistakes

- **Defaulting an unknown-reversibility step to autonomous "for now," planning to tighten it later.** This is the exact failure this skill exists to prevent -- an unknown must read as a ceiling on classification from the start, not a temporary convenience.
- **Letting a low apparent cost override the reversibility floor.** A step that "seems minor" is still capped at Approval Required if its reversibility is genuinely unknown; the cost side of the input doesn't unlock a lower classification when the reversibility side is missing.
- **Treating a large number of clean runs as proof that an unresolved unknown was actually safe.** Volume of runs is evidence about the agent's behavior under the classification it was given, not evidence that a still-unknown reversibility fact has been resolved.
- **Classifying the whole workflow instead of each step.** A single irreversible, high-cost step buried in an otherwise low-stakes sequence gets averaged away if classification happens at the workflow level.
- **Writing an "approval required" step that nobody can actually block at** -- a review-only notification or an approval gate with no enforced pause is a Review classification wearing an Approval Required label.
- **Skipping a tier when loosening classification** -- moving a Blocked step straight to Autonomous, or Approval Required straight to Autonomous, without passing through the intermediate tier's own graduation criteria.

## Practice Questions

- For every step classified Autonomous, can I point to the specific reversibility and cost evidence that put it there -- or did I land there because reversibility was actually unknown and I didn't apply the floor?
- If a graduation from Approval Required to Review is being proposed today, is it because reversibility was actually resolved and verified, or only because the step has run N times without incident while the reversibility question itself was never answered?
- Which Blocked step's escalation path names an owner who, if asked right now, would recognize that they hold this responsibility?

## Improvement Loop

After a workflow's classification table goes live, track any incident that occurs at a step classified Autonomous or Review -- a miss there is a signal that the classification logic (not just this one workflow's table) needs tightening, especially if the step's reversibility or cost was marked known but turns out to have been misjudged. Separately, track every step that graduated to a lighter classification: for each one, confirm whether the graduation followed resolving a genuine unknown (a sign the process is working) or was granted on run-count alone while an unknown stayed unresolved (a sign this skill's own discipline was not actually followed, and the step should be reclassified back down until the unknown is resolved).
