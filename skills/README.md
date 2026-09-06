# Skills for the PM Competency Model

This folder holds Claude Code skills that support the competency model used in this repository (see [docs/pm-competency-model.md](../docs/pm-competency-model.md)). Together they form the `product-leadership-skills` Claude Code plugin — see [../INSTALLATION.md](../INSTALLATION.md) to install the whole set at once.

The goal of these skills is to help product leaders and teams:

- grow against clear product competencies
- align expectations between managers, peers, and direct reports
- use consistent evaluation language in reviews and feedback
- connect hiring and interview questions to the same success criteria
- improve capability over time with structured practice and reflection

Each skill maps to one or more sub-competencies and ends with practice questions and an improvement loop, so its output can double as evidence in coaching, review, or hiring conversations.

## Available skills

24 skills total: the original 7 core skills, plus 17 shipped from the Wave 1 expansion (`docs/superpowers/plans/2026-08-23-product-leadership-skills-expansion.md`) across Discovery & Definition, Prioritization & Decision Support, Stakeholder & Leadership, Analytics, and AI-native Product Workflows.

| Skill | Use case | Competency |
| --- | --- | --- |
| [synthesize-research](synthesize-research/SKILL.md) | Turn interview notes, survey responses, or support tickets into ranked, attributed findings | Customer Insight — Voice of the Customer, Fluency with Data |
| [user-research](user-research/SKILL.md) | Plan, run, and synthesize a user research study end to end | Customer Insight — Voice of the Customer, Fluency with Data |
| [write-feature-spec](write-feature-spec/SKILL.md) | Turn a feature idea, stakeholder ask, or research finding into an actionable spec with scope and success criteria | Product Execution — Feature Specification |
| [stakeholder-alignment-brief](stakeholder-alignment-brief/SKILL.md) | Pre-read for a meeting that needs to move stakeholders from informed to aligned on a decision | Influencing People — Stakeholder Management |
| [prep-competency-review](prep-competency-review/SKILL.md) | Prepare a performance review, coaching conversation, or interview rubric against the competency model | Cross-cutting — all four categories |
| [build-dashboard](build-dashboard/SKILL.md) | Build a self-contained HTML dashboard with KPI cards, charts, filters, and tables | Product Strategy — Business Outcome Ownership, Strategic Impact |
| [data-visualization](data-visualization/SKILL.md) | Choose chart types and apply design principles for any chart another skill needs | Support skill — backs Fluency with Data and Strategic Impact |
| [opportunity-framing](opportunity-framing/SKILL.md) | Turn a synthesized finding or raw stakeholder signal into a framed opportunity (who / problem / why now) | Customer Insight — Voice of the Customer; Product Strategy — Strategic Impact |
| [problem-validation](problem-validation/SKILL.md) | Check the evidence strength behind a stated problem before it consumes roadmap time | Customer Insight — Fluency with Data; Product Strategy — Business Outcome Ownership |
| [write-intent](write-intent/SKILL.md) | Turn a validated opportunity into a short, approvable product intent doc before spec work starts | Product Strategy — Product Vision & Roadmapping; Product Execution — Feature Specification |
| [define-success-metrics](define-success-metrics/SKILL.md) | Define the specific, instrumented metrics that will judge an intent or spec | Customer Insight — Fluency with Data; Product Strategy — Business Outcome Ownership |
| [identify-product-risks](identify-product-risks/SKILL.md) | Surface technical, market, UX, compliance, and adoption risks in a spec or plan before it ships | Product Execution — Product Quality; Product Strategy — Strategic Impact |
| [write-decision-brief](write-decision-brief/SKILL.md) | Write up any product decision — options, trade-offs, recommendation — before it's made | Product Strategy — Strategic Impact; Influencing People — Stakeholder Management |
| [compare-options](compare-options/SKILL.md) | Score 2+ concrete options side-by-side against explicit, confirmed criteria | Product Strategy — Strategic Impact; Customer Insight — Fluency with Data |
| [prepare-prioritization](prepare-prioritization/SKILL.md) | Turn a candidate backlog into a scored, flagged worksheet ready for a prioritization session | Product Strategy — Business Outcome Ownership; Product Execution — Product Delivery |
| [executive-update](executive-update/SKILL.md) | Turn project/product status into a concise executive-facing update: progress, metrics, risks, ask | Influencing People — Managing Up; Product Strategy — Business Outcome Ownership |
| [decision-log](decision-log/SKILL.md) | Append to or query a durable, append-only log of product decisions and their rationale | Influencing People — Stakeholder Management; Product Strategy — Strategic Impact |
| [metric-definition](metric-definition/SKILL.md) | Produce a rigorous metric definition (formula, edge cases, owner), or check one is actually computable | Customer Insight — Fluency with Data |
| [experiment-analysis](experiment-analysis/SKILL.md) | Read a concluded A/B test with statistical validity before recommending ship/kill/extend | Customer Insight — Fluency with Data; Product Strategy — Business Outcome Ownership |
| [context-audit](context-audit/SKILL.md) | Audit a bounded set of docs for stale context, conflicting definitions, and missing source-of-truth designations | Customer Insight — Fluency with Data; Product Execution — Product Quality |
| [agent-readiness-review](agent-readiness-review/SKILL.md) | Assess whether a described workflow is safe to hand to an autonomous agent, before it's built | Product Strategy — Strategic Impact; Product Execution — Product Quality |
| [ai-feature-risk-review](ai-feature-risk-review/SKILL.md) | Review an AI-powered feature before shipping for user harm, incorrect-action risk, data exposure, and failure recovery | Product Execution — Product Quality; Product Strategy — Strategic Impact |
| [eval-plan](eval-plan/SKILL.md) | Turn an AI feature's expected behavior into measurable eval test cases | Product Execution — Product Quality; Customer Insight — Fluency with Data |
| [human-in-the-loop-design](human-in-the-loop-design/SKILL.md) | Classify every step of an agent-driven workflow as autonomous, reviewed, approval-required, or blocked | Product Strategy — Strategic Impact; Product Execution — Product Quality |

`user-research` plans and runs a study; `synthesize-research` analyzes the results once it's done — use them together. `opportunity-framing` → `problem-validation` → `write-intent` → `write-feature-spec` is the discovery-to-spec chain (see [examples/demo-chain/README.md](../examples/demo-chain/README.md)). `build-dashboard` produces a stakeholder-facing artifact; `data-visualization` is the reference it (and other skills) draw on for a single chart. `agent-readiness-review`, `ai-feature-risk-review`, and `human-in-the-loop-design` all default unstated reversibility/autonomy to the stricter classification, never the permissive one.

Machine-readable version: [skills/competencies.yaml](competencies.yaml).

Add new skills here as the repository grows. When adding one, name it for what it produces, tie it to the specific sub-competency(ies) it exercises, and give it practice questions and an improvement loop so it stays consistent with the skills above.
