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
