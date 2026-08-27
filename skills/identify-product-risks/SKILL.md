---
name: identify-product-risks
description: Systematically surface risks (technical, market, UX, compliance, adoption) in a spec or plan before it ships, producing a scored risk register with owners and mitigations. Use during spec review, before a pre-launch go/no-go, when a stakeholder asks "what could go wrong," or whenever a spec or plan is about to move into build without a structured risk pass.
argument-hint: "<spec or plan to review, plus known constraints and compliance/legal context if any>"
---

<!-- sourcing: drafted-fresh -->
<!--
  Sourcing notes (per skills/CONTRIBUTING.md "Sourcing a new skill"):
  Searched (a) Anthropic's official examples (anthropics/skills repo, README) for a
  risk-register or product-risk skill -- none found there specifically for product/spec
  risk review. Searched (b) GitHub code/repo search for "risk register" + "claude skill",
  "product risk" claude skill, and general web search for awesome-claude-skills /
  awesome-claude-code lists plus '"product risk" claude skill' and '"risk register"
  prompt template product management'. Evaluated the closest candidates found:
    - namthhl/claude-skill-risk-register-template -- well-built, but scoped to living
      risk registers for long-running engineering systems (its own "When NOT to trigger"
      section excludes one-off spec review); wrong domain to adapt cleanly.
    - gtmagents/gtm-agents (risk-playbooks skill) -- product-launch risk categories are
      relevant, but the skill is a thin outline with no required-inputs list, no stated
      missing-input behavior, and no constraints section.
    - travisjneuman/.claude (risk-management skill) -- enterprise/ERM risk management
      (COSO, third-party vendor risk, board reporting); wrong altitude for a spec-level
      product risk pass.
    - mohitagw15856/pm-claude-skills (risk-register skill) -- structurally closest (L x I
      scoring, RAG status, categories including compliance), but part of a 1000+-skill
      mass-generated dump with no stated missing-input behavior and no constraint against
      turning an unknown compliance context into a silent gap -- exactly what this task
      brief requires as an explicit, checkable rule.
    - pratikshadake/claude-product-management-skills (launch-readiness skill) -- adjacent
      but a generic launch checklist, not a scored risk register.
  None specified inputs + explicit missing-input behavior + constraints + output structure
  to the bar this repo requires (see skills/CONTRIBUTING.md), so this skill is drafted
  fresh, using synthesize-research and define-success-metrics as style references.
-->

# Identify Product Risks

Turn a spec or plan into a scored risk register -- what could go wrong, how likely, how bad, and who owns closing the gap -- before it ships.

## Usage

```
/identify-product-risks $ARGUMENTS
```

## Competency Connection

This skill is the practical exercise of two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Product Execution > Product Quality** -- the model defines this as identifying, prioritizing, and resolving technical, functional, and business quality issues across all devices, points of sale, and use cases, and notes that quality rarely moves metrics in an obviously attributable way, which is exactly why it gets deprioritized until it erodes trust. A risk register produced before launch, with each risk scored and assigned an owner, is direct evidence a PM did this identification and prioritization work deliberately rather than discovering quality issues in production.
- **Product Strategy > Strategic Impact** -- the model defines this as understanding and contributing to business strategy and bringing it to fruition through consistent delivery of business outcomes. Naming market, compliance, and adoption risks (not just technical ones) before a launch commits resources is what keeps a delivery decision connected to the business outcome it's supposed to protect, rather than treating "shipped on schedule" as success on its own.

## Required Inputs

- **The spec or plan being reviewed** -- a `write-feature-spec` output, a `write-intent` output, or an equivalent description of what's being built, for whom, and what it touches (data, user flows, systems).
- **Known constraints** -- technical, resourcing, timeline, or organizational limits already established for this work.
- **Compliance/legal context** -- specifically: whether compliance or legal has reviewed this spec, and if so, what they found. "Not reviewed" or "unknown" are acceptable answers to capture, but the answer must be captured, not assumed.

## If Inputs Are Missing

- **No spec or plan provided**: ask for it. A risk register produced against a vague topic instead of a scoped spec/plan has nothing concrete to check for failure modes -- there's no user flow, data touchpoint, or dependency to actually interrogate.
- **Compliance/legal context unknown (the core case this skill exists to handle)**: never silently skip the Compliance category and never silently assume there's no compliance concern. Add an explicit risk register entry in the Compliance category stating that legal/compliance review status is unknown, with likelihood and impact estimated from what the spec touches (user data, payments, regulated categories, new jurisdictions), and name "confirm compliance review status" as the mitigation with an owner. This is a mandatory rule -- see Constraints.
- **Known constraints not stated**: proceed, but write "no constraints stated" rather than inventing plausible-sounding ones, and note that unstated constraints (e.g. an unconfirmed deadline) are themselves a source of schedule risk.

## Process

1. **Restate the spec or plan.** One or two sentences: what's being built, for whom, and what it touches -- user flows, systems, data.
2. **Establish compliance/legal context explicitly.** Ask (or read from the input) whether compliance/legal has looked at this. If unknown, do not proceed as though the answer were "no concern" -- carry it forward as an open risk category per the rule above.
3. **Sweep each risk category in turn**, generating candidate risks from the spec's actual content (not generic boilerplate): Technical (build/integration/performance/reliability), Market (competitive response, timing, demand), UX (usability, discoverability, accessibility), Compliance (regulatory, privacy, legal, contractual), Adoption (rollout, training, change management, incentive misalignment).
4. **Score each candidate risk** on likelihood (Low/Medium/High) and impact (Low/Medium/High), based on what the spec and known constraints actually say -- not a default middle score used to avoid a judgment call.
5. **Assign category, mitigation, and owner** to each risk that clears the register (see Constraints for what doesn't clear it). A mitigation must be a specific action, not "monitor closely." An owner must be a role or name, not "the team."
6. **Separate out-of-scope risks explicitly.** List risks that were considered but are being deliberately left for a later pass (e.g. post-launch monitoring risks, risks owned by a different team's spec), and say why each is out of scope now rather than silently dropping them.
7. **Rank the top 3 by likelihood x impact** and call them out separately from the full register, so a reviewer with five minutes knows what to look at first.
8. **Name the review checkpoint.** Who, by role, must review this register (and specifically confirm or close the compliance-unknown entry, if present) before the spec is treated as ready to build.

## Constraints

- **Unknown compliance/legal context is always an explicit open risk, never a silent gap.** If nobody has confirmed whether compliance or legal has reviewed a spec that plausibly touches regulated data, payments, a regulated user category, or crosses a jurisdiction, this skill must add a Compliance-category risk register entry stating that review status is unknown -- it must never omit the Compliance category, and never assume "not mentioned" means "not a concern." This is the one rule in this skill that is never optional, regardless of how confident the rest of the spec looks.
- **A risk without a specific mitigation and a named owner does not belong in the register.** "Keep an eye on this" is not a mitigation, and "the team" is not an owner. A candidate risk that can't clear both bars either needs more investigation before it's added, or belongs in the out-of-scope section with a reason.
- **Do not pad the register with generic, boilerplate risks that aren't grounded in what this specific spec actually does.** Every entry must trace to something concrete in the spec, plan, or known constraints -- a risk that would apply identically to any spec in the company is not doing real work here.
- **Do not default every score to Medium to avoid a judgment call.** Likelihood and impact must reflect an actual read of the spec and constraints; a register where every row scores the same is a sign the scoring step was skipped, not that the risks are genuinely balanced.
- **This skill surfaces risks and proposes mitigations and owners for a human team to act on -- it does not unilaterally block a launch.** The Top 3 and the full register are inputs to a go/no-go decision made by the named reviewer(s), not a decision this skill makes on its own.

## Output Format

```
# Risk Register: [spec or plan name]

## Risk Register

| Risk | Likelihood | Impact | Category | Mitigation | Owner |
|------|-----------|--------|----------|------------|-------|
| [Specific risk grounded in the spec] | [Low/Medium/High] | [Low/Medium/High] | [Technical/Market/UX/Compliance/Adoption] | [Specific action] | [Role or name] |
(repeat for each risk that clears the register)

## Risks Explicitly Out of Scope for This Pass (and why)
- [Risk] -- out of scope because [reason: owned by another team's spec, post-launch
  monitoring concern, insufficient information to score yet, etc.]
(repeat)

## Top 3 by (Likelihood x Impact)
1. [Risk] -- [why it ranks here]
2. [Risk] -- [why it ranks here]
3. [Risk] -- [why it ranks here]

## Review Checkpoint
[Named role(s) who must review this register -- and specifically confirm or close any
compliance-unknown entry -- before the spec is treated as ready to build]
```

## Review Checkpoints

- A human must confirm each risk's likelihood/impact score against their own read of the spec -- this skill proposes scores from the spec's content, it does not have ground truth on the team's actual technical or market context.
- Where a Compliance-category entry flags review status as unknown, a human (compliance, legal, or the named owner) must actually resolve it -- confirm reviewed-and-clear, reviewed-with-findings, or genuinely out of scope -- before this register is treated as closing that risk. This skill can only flag the gap, not close it.
- The named role(s) in Review Checkpoint must actually review the full register, not just the Top 3, before the spec is treated as ready to build -- this skill surfaces and scores risks, it does not decide whether the spec is safe to ship.

## Common Mistakes

- **Treating an unconfirmed compliance/legal review as "no concern" and leaving the Compliance category empty.** If nobody has actually confirmed review status, that absence is itself the risk to register -- not a reason to skip the category.
- **Rows with a mitigation of "monitor" and an owner of "the team."** Neither is specific enough to act on; both are signs the risk wasn't actually investigated before being added.
- **A register full of boilerplate risks that would apply to any spec.** "Might have bugs" or "users might not adopt it" without grounding in what this spec specifically does isn't identification -- it's padding.
- **Every risk scored Medium/Medium.** Usually means the scoring step was skipped rather than that every risk is genuinely balanced.
- **Silently dropping a risk instead of listing it as out of scope with a reason.** A reviewer can't tell "considered and deferred" from "never considered" unless the out-of-scope section says so explicitly.
- **Presenting the Top 3 as a launch decision rather than an input to one.** This skill ranks and surfaces; the named reviewer(s) decide whether to launch.

## Practice Questions

- Could every mitigation in this register be handed to its named owner as a real next action -- or would some of them just get "how?" as a reply?
- If compliance/legal review status was unknown going in, does the register make that unmistakably visible to a reviewer skimming the Top 3 and the Compliance rows -- or is it buried or missing?
- Do any two risks in the register read identically to what would appear on a completely different spec? If so, were they actually derived from this spec, or copied in as boilerplate?

## Improvement Loop

After launch, revisit the register: which risks actually materialized, which mitigations held, which owners actually closed their item before it became a problem, and which risks this pass missed entirely. Feed specific misses back into how aggressively this skill sweeps each category next time -- especially whether a compliance-unknown entry got resolved before launch or slipped through unresolved -- so "Product Quality" and "Strategic Impact" evidence stays grounded in what actually happened, not just what was predicted.
