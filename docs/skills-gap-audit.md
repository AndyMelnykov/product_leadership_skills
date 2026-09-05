# Skills Gap Audit

> Sourced from `docs/vision/product-leadership-skills-vision.md` (currently a placeholder skeleton — see that file's status comment) and the implementation plan `docs/superpowers/plans/2026-08-23-product-leadership-skills-expansion.md`. Where the vision doc itself is not yet filled in, the catalog-coverage table below is derived from the plan's Blocks F-K, which already name every Wave 1 skill and its group; this is noted per-row rather than presented as if read from the vision doc directly.

## Contract-coverage table

One row per existing skill, one column per contract element. Legend: ✅ present and explicit · ⚠️ present in substance but not explicit/labeled · ❌ absent. Assessed by rereading each `skills/<name>/SKILL.md` in full on 2026-08-24.

| Skill | Purpose | Trigger | Inputs | Missing-input behavior | Process | Constraints | Output | Review | Evaluation | `references/` | `examples/` | `evals/` |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| synthesize-research | ✅ | ✅ | ✅ (Step 1: asks research type, sample size, hypothesis, decision) | ⚠️ (asks questions; no stated fallback if unanswered) | ✅ (numbered Steps 1-5) | ⚠️ ("Tips" list at bottom, not a `## Constraints` heading) | ✅ | ⚠️ ("Review and Extend" is about follow-ups, not an approval checkpoint) | ❌ | ❌ | ❌ | ❌ |
| write-feature-spec | ✅ | ✅ | ✅ (Step 1: Clarify the Input) | ⚠️ ("if the input is a hunch, say so explicitly" — partial, not comprehensive) | ✅ (numbered Steps 1-5) | ⚠️ ("Common Mistakes", not `## Constraints`) | ✅ (explicit template) | ❌ | ❌ | ❌ | ❌ | ❌ |
| stakeholder-alignment-brief | ✅ | ✅ | ✅ (Steps 1-2) | ⚠️ ("If unclear, say so" for owner only — partial) | ✅ (numbered Steps 1-4) | ⚠️ ("Common Mistakes") | ✅ (explicit template) | ❌ | ❌ | ❌ | ❌ | ❌ |
| user-research | ✅ | ✅ (frontmatter lists explicit trigger phrases) | ❌ (no section asks for research goal or participant profile) | ❌ (nothing states what to do absent a stated goal) | ⚠️ (methods table + guide structure, not numbered steps) | ❌ | ⚠️ ("Deliverables" lists outputs, not a structured format) | ❌ | ❌ | ❌ | ❌ | ❌ |
| data-visualization | ✅ | ✅ | ❌ (reference/support skill; no inputs section) | ❌ | ⚠️ (organized as reference guide, not process steps) | ⚠️ ("When NOT to Use Certain Charts" + "Accuracy" are substantive constraints, unlabeled) | ❌ (code patterns instead of an output-format section) | ❌ | ❌ | ❌ | ❌ | ❌ |
| build-dashboard | ✅ | ✅ | ⚠️ (Step 1 "Understand the Dashboard Requirements", not labeled Required Inputs) | ⚠️ (explicit fallback for missing *data* — sample dataset — but not for other missing inputs) | ✅ (numbered Steps 1-7) | ❌ (no vanity-metric or other guardrail; plan's Task 8 confirms this gap) | ✅ (base template, KPI card pattern) | ❌ | ❌ | ❌ | ❌ | ❌ |
| prep-competency-review | ✅ ("Why This Skill Exists") | ✅ | ✅ (Step 1: Establish the Purpose and Person) | ✅ ("Skipping categories with no evidence" — absence of evidence noted as a gap, not silently omitted) | ✅ (numbered Steps 1-4) | ⚠️ ("Common Mistakes") | ✅ (explicit template) | ⚠️ ("Alignment Check" in the output partially serves this, not a named review checkpoint) | ❌ | ❌ | ❌ | ❌ |

## Catalog-coverage table

One row per skill named in the plan's seven Core skill groups (Block F-K naming; the vision doc's own "Core skill groups" section is currently a TODO stub — see status note above).

| Skill group | Skill | Exists in repo? | Repo skill name (if any) | Status |
|---|---|---|---|---|
| Discovery & research | User research planning/execution | ✅ | `user-research` | Built |
| Discovery & research | Research synthesis | ✅ | `synthesize-research` | Built |
| Discovery & research | Opportunity framing | ❌ | — | Wave 1 backlog (Task 12) |
| Discovery & research | Problem validation | ❌ | — | Wave 1 backlog (Task 13) |
| Discovery & research | Interview plan | ❌ | — | Later backlog (Task 30) |
| Discovery & research | JTBD synthesis | ❌ | — | Later backlog (Task 30) |
| Discovery & research | Competitor analysis | ❌ | — | Later backlog (Task 30) |
| Product definition | Feature spec | ✅ | `write-feature-spec` | Built |
| Product definition | Product intent | ❌ | — | Wave 1 backlog (Task 14: `write-intent`) |
| Product definition | Success-metric definition | ❌ | — | Wave 1 backlog (Task 15: `define-success-metrics`) |
| Product definition | Product risk identification | ❌ | — | Wave 1 backlog (Task 16: `identify-product-risks`) |
| Product definition | Problem decomposition | ❌ | — | Later backlog (Task 30: `decompose-product-problem`) |
| Product definition | Assumption mapping | ❌ | — | Later backlog (Task 30: `assumption-mapping`) |
| Prioritization & decision support | Decision brief (general) | ❌ | — | Wave 1 backlog (Task 17: `write-decision-brief`) |
| Prioritization & decision support | Options comparison | ❌ | — | Wave 1 backlog (Task 18: `compare-options`) |
| Prioritization & decision support | Prioritization session prep | ❌ | — | Wave 1 backlog (Task 19: `prepare-prioritization`) |
| Prioritization & decision support | Roadmap trade-off analysis | ❌ | — | Later backlog (Task 30: `roadmap-tradeoff-analysis`) |
| Stakeholder work | Stakeholder alignment brief | ✅ | `stakeholder-alignment-brief` | Built |
| Stakeholder work | Executive update | ❌ | — | Wave 1 backlog (Task 20: `executive-update`) |
| Stakeholder work | Decision log | ❌ | — | Wave 1 backlog (Task 21: `decision-log`) |
| Analytics | Static data visualization | ✅ | `data-visualization` | Built |
| Analytics | Interactive dashboard | ✅ | `build-dashboard` | Built |
| Analytics | Metric definition | ❌ | — | Wave 1 backlog (Task 22: `metric-definition`) |
| Analytics | Experiment analysis | ❌ | — | Wave 1 backlog (Task 23: `experiment-analysis`) |
| Analytics | Experiment plan generation | ❌ | — | Later backlog (Task 30: `generate-experiment-plan`) |
| Analytics | Funnel analysis | ❌ | — | Later backlog (Task 30: `funnel-analysis`) |
| Analytics | Retention analysis | ❌ | — | Later backlog (Task 30: `retention-analysis`) |
| Analytics | AI product metrics | ❌ | — | Later backlog (Task 30: `AI-product-metrics`) |
| Leadership | Competency review prep | ✅ | `prep-competency-review` | Built |
| Leadership | PM coaching plan | ❌ | — | Later backlog (Task 30: `PM-coaching-plan`) |
| Leadership | Team skill-gap analysis | ❌ | — | Later backlog (Task 30: `team-skill-gap-analysis`) |
| Leadership | Product org review | ❌ | — | Later backlog (Task 30: `product-org-review`) |
| Leadership | Product review prep | ❌ | — | Later backlog (Task 30: `product-review-prep`) |
| Leadership | Launch readiness review | ❌ | — | Later backlog (Task 30: `launch-readiness-review`) |
| AI-native product workflows | Context audit | ❌ | — | Wave 1 backlog (Task 24: `context-audit`) |
| AI-native product workflows | Agent readiness review | ❌ | — | Wave 1 backlog (Task 25: `agent-readiness-review`) |
| AI-native product workflows | AI feature risk review | ❌ | — | Wave 1 backlog (Task 26: `AI-feature-risk-review`) |
| AI-native product workflows | Eval plan | ❌ | — | Wave 1 backlog (Task 27: `eval-plan`) |
| AI-native product workflows | Human-in-the-loop design | ❌ | — | Wave 1 backlog (Task 28: `human-in-the-loop-design`) |

## Findings

- **Most commonly missing contract elements**, confirmed by inspection above: `evals/` (0 of 7 skills have any), `examples/` (0 of 7), an explicit `## Review Checkpoints`-style section (0 of 7 name one; two have adjacent-but-unlabeled content), and an explicit `## Constraints` heading (0 of 7 — five have constraint content under a different heading like "Common Mistakes" or "Tips," and two have none at all). This confirms the plan's expectation.
- **Missing-input behavior** is inconsistent rather than uniformly absent: `prep-competency-review` states one explicitly (absence-of-evidence handling), three skills have partial/implicit coverage, and `user-research` and `data-visualization` have none.
- **Skill groups with zero coverage today**: AI-native product workflows (0 of 5 planned Wave 1 skills exist). Analytics and Leadership each have their flagship skill built but 4-6 adjacent skills in the group still missing — consistent with the plan's expectation that these two groups carry most of the remaining gap.
- **Weakest existing skills against the contract**: `user-research` and `data-visualization` are the two skills with no Inputs/Missing-input/Constraints/Output-format sections at all — both are earlier or support-style skills predating the contract, and Block C's retrofit procedure will need to add substance, not just headings, to close their gaps (their retrofit tasks in the plan only scope `evals/`, so this is a note for whoever executes Block C, not something this audit resolves).

## Backlog — not yet built

Every vision-doc skill still uncovered after Wave 1 (Blocks F-K, Tasks 12-28), with an honest call on why it wasn't built now: either it ranked below what Blocks F-K covered, or it overlaps heavily with an already-built skill and should be scoped only after real usage shows the built skill isn't enough (YAGNI) rather than built speculatively now.

| Skill | Skill group | Why not Wave 1 |
|---|---|---|
| `competitor-analysis` | Discovery & research | Lower priority than Blocks F-K's discovery work — Wave 1 built the internal signal-to-opportunity pipeline (`opportunity-framing`, `problem-validation`) but didn't reach external competitive-landscape research. |
| `JTBD-synthesis` | Discovery & research | YAGNI — `synthesize-research` already turns raw findings into structured insight; a JTBD-specific synthesis lens should be split out only once real usage shows the generic synthesis process can't produce a proper jobs framing. |
| `decompose-product-problem` | Product definition | Lower priority — Wave 1's product-definition skills (`opportunity-framing`, `problem-validation`, `write-intent`) frame and validate a problem but none does formal issue-tree decomposition of a large or ambiguous one; not enough signal yet that teams need it as a separate step. |
| `generate-experiment-plan` | Analytics | Lower priority, not overlap — `experiment-analysis` reads a *concluded* experiment; the pre-registration/design half (hypothesis, sample-size, guardrails, duration) is a genuine adjacent gap Wave 1 didn't reach, tracked here rather than assumed covered. |
| `roadmap-tradeoff-analysis` | Prioritization & decision support | YAGNI — `compare-options` is explicitly built as the reusable scoring building block "a roadmap trade-off analysis calls on for its own options table," and `write-decision-brief` already wraps that into a recommendation; a roadmap-specific skill should wait until composing those two by hand proves insufficient. |
| `assumption-mapping` | Product definition | YAGNI — `problem-validation` already scores evidence strength behind a stated problem and `identify-product-risks` already surfaces and scores risks with owners/mitigations; assumption mapping covers much of the same desirability/feasibility/viability ground and should be scoped only if usage shows a real gap between the two. |
| `product-review-prep` | Leadership | YAGNI — `executive-update` already turns status into a concise, audience-facing update covering progress, metrics, risks, and asks; a product-review-specific variant should wait until a recurring product-review format proves distinct enough from an exec update to need its own skill. |
| `launch-readiness-review` | Leadership | YAGNI — `identify-product-risks` already names "before a pre-launch go/no-go" as a stated use case and produces a scored risk register with owners and mitigations; a separate launch-readiness skill overlaps heavily with it pending evidence that launch review needs more than a risk pass. |
| `funnel-analysis` | Analytics | YAGNI — `metric-definition` (rigorous per-metric formulas) and `build-dashboard` (multi-chart, filterable views) already cover defining and visualizing funnel-step metrics; a dedicated funnel-diagnosis skill should wait until teams need drop-off-cause analysis those two don't provide. |
| `retention-analysis` | Analytics | YAGNI, same reasoning as `funnel-analysis` — `metric-definition` and `build-dashboard` already cover defining and displaying a retention or cohort metric; a dedicated analysis skill (cohort curves, churn-driver diagnosis) should be scoped only once that gap is felt in practice. |
| `interview-plan` | Discovery & research | YAGNI — `user-research`'s own description states it "plans and runs a study," which already covers interview planning; a narrower interview-only skill should be split out only if the general research-planning skill proves too broad for interview-specific prep. |
| `PM-coaching-plan` | Leadership | YAGNI — `prep-competency-review`'s description explicitly covers preparing "a coaching conversation" from the same competency evidence used for a review; a separate coaching-plan skill overlaps directly with it pending evidence the two need to diverge. |
| `team-skill-gap-analysis` | Leadership | YAGNI — `prep-competency-review` plus `competencies.yaml` already supply per-person competency evidence and taxonomy; aggregating that across a team is a rollup of existing building blocks, not yet justified as its own skill. |
| `product-org-review` | Leadership | Lower priority — no Wave 1 skill addresses org-level structure or process health (the closest, `prep-competency-review`, is scoped to one person, and `executive-update` to one initiative); genuinely uncovered, but ranked below Blocks F-K's individual- and decision-level gaps. |
| `AI-product-metrics` | Analytics | YAGNI — `metric-definition` already produces rigorous, source-traceable metric definitions for any named metric; an AI-specific variant should be split out only once real AI features show `metric-definition` can't handle things like cost-per-query, groundedness, or override-rate without dedicated guidance (distinct from `eval-plan`, which covers pre-launch quality test cases, not ongoing production metrics). |
