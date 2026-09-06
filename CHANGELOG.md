# Changelog

All notable changes to this plugin are recorded here.

## [1.1.0] — 2026-09-06

### What changed

- Standardized the skill contract across all skills: every `SKILL.md` now states Purpose, Trigger, Inputs, Missing-input behavior, Process, Constraints, Output, Review, and Evaluation, via a shared template (`skills/_TEMPLATE/SKILL.md`) and contributor guide (`skills/CONTRIBUTING.md`).
- Retrofitted the original 7 skills (`synthesize-research`, `user-research`, `write-feature-spec`, `stakeholder-alignment-brief`, `prep-competency-review`, `build-dashboard`, `data-visualization`) with explicit `## Constraints` / `## If Inputs Are Missing` sections and YAML eval cases; added golden strong/weak examples to the two flagship skills (`synthesize-research`, `write-feature-spec`).
- Added 17 new skills across five groups: Discovery & Definition (`opportunity-framing`, `problem-validation`, `write-intent`, `define-success-metrics`, `identify-product-risks`), Prioritization & Decision Support (`write-decision-brief`, `compare-options`, `prepare-prioritization`), Stakeholder & Leadership (`executive-update`, `decision-log`), Analytics (`metric-definition`, `experiment-analysis`), and AI-native Product Workflows (`context-audit`, `agent-readiness-review`, `ai-feature-risk-review`, `eval-plan`, `human-in-the-loop-design`) — bringing the catalog to 24 skills total.
- Added `skills/competencies.yaml`, a machine-readable skill-to-competency map cross-checked against every skill's prose "Competency Connection" section.
- Added an end-to-end demo chain (`examples/demo-chain/`) showing one research signal flow through `synthesize-research` → `opportunity-framing` → `write-intent` → `write-feature-spec` → `stakeholder-alignment-brief` as durable artifacts, each stage consuming the last.
- Refreshed root and `skills/` READMEs: the vision doc's positioning statement, a "What makes it different" section, the full 24-skill catalog table, and corrected skill-count references.

### Why

Closes the gap identified in `docs/skills-gap-audit.md` between the repo's original 7-skill set and the full vision described in `docs/vision/product-leadership-skills-vision.md` — a testable, evidence-based, competency-linked library of product-leadership agent skills, not a prompt collection. Tracked in full: `docs/superpowers/plans/2026-08-23-product-leadership-skills-expansion.md`.

### Expected behavior impact

Additive and stricter-internal-contract only — the original 7 skills behave the same for users as before this expansion; nothing here is a breaking change. 17 new skills are now installed as part of the same plugin.

## [1.0.0]

Initial release: 7 skills (`synthesize-research`, `user-research`, `write-feature-spec`, `stakeholder-alignment-brief`, `prep-competency-review`, `build-dashboard`, `data-visualization`) packaged as an installable Claude Code plugin, mapped to the PM competency model.
