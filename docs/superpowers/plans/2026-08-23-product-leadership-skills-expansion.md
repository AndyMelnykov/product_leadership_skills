# Product Leadership Skills Expansion Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Evolve this repo from "7 good SKILL.md files + a competency model" into the full vision described in the attached positioning doc — a testable, evidence-based, competency-linked library of product-leadership agent skills, without collapsing into a prompt collection.

**Architecture:** Keep the existing Claude Code plugin shape (`skills/<name>/SKILL.md` with `name`/`description`/`argument-hint` frontmatter, bundled via `.claude-plugin/`) as the load-bearing format — it already works and is installed via `/plugin`. Layer the richer "skill anatomy" (`references/`, `examples/`, `evals/`, `templates/`) on top of that format only where a skill has enough durable framework material or eval cases to justify it, rather than forcing empty boilerplate folders onto every skill. New skills are sourced by searching for existing public examples first (Anthropic's own skill examples, community skill/prompt libraries) and only hand-authored when nothing suitable is found, then always brought up to this repo's skill-contract bar and re-tied to the PM competency model.

**Tech Stack:** Markdown (SKILL.md, references, examples), YAML frontmatter, YAML eval case files, Claude Code plugin manifest (`.claude-plugin/plugin.json`, `marketplace.json`), git.

**Spec:** `05-product-leadership-skills.md` (the attached positioning doc). It is not currently version-controlled in this repo — Task 0 below fixes that by committing it as the canonical vision doc, since every later block argues from it.

## Global Constraints

- Preserve the existing SKILL.md frontmatter contract (`name`, `description`, `argument-hint`) exactly as used by the 7 existing skills — new/retrofitted skills must stay installable via the existing `/plugin` flow. Do not invent a second, incompatible skill format.
- Every skill (new or retrofitted) must be traceable to the 9-part skill contract from the spec: Purpose, Trigger, Inputs, Missing input behavior, Process, Constraints, Output, Review, Evaluation. It doesn't need 9 literal headers, but a reader must be able to point to where each is answered.
- Every skill must map to at least one sub-competency in `docs/pm-competency-model.md`, following the existing "Competency Connection" convention (see `skills/synthesize-research/SKILL.md:17-28`).
- Do not invent new competency categories. Reuse exactly the four categories / twelve sub-competencies already defined in `docs/pm-competency-model.md`.
- Before hand-authoring any new skill, search for an existing, freely reusable example first (see Block E's Search Procedure). Only draft from scratch if nothing suitable is found. Note the search outcome (adapted-from-X, or none-found-drafted-fresh) in an HTML comment at the top of the skill's SKILL.md so the sourcing decision stays inspectable.
- Never let a skill's Process section produce a recommendation, rating, or decision directly from weak/absent evidence — every skill must have an explicit "when evidence is thin, do X" rule (mirrors the source doc's "must not convert weak evidence directly into recommendations" rule and the existing competency-review skill's evidence-vs-impression distinction).
- Do not create empty `references/`, `examples/`, `templates/`, or `evals/` folders "for completeness." Add a subfolder only when it holds real content produced by the task that creates it.
- Avoid list (from spec, self-check before closing any block): the repo must not become a prompt collection, a PM-quote library, a set of generic templates, a competency encyclopedia, or a place that claims agents replace product judgment.

---

## File Structure Overview

```
docs/
  vision/
    product-leadership-skills-vision.md   # Task 0 — the spec, versioned
  skills-gap-audit.md                      # Task 1 — contract + catalog gap matrix
skills/
  _TEMPLATE/
    SKILL.md                               # Task 2 — contract skeleton for new skills
  CONTRIBUTING.md                          # Task 2 — anatomy, source hierarchy, context rules, human/agent boundary
  <existing-skill>/
    SKILL.md                               # Modify — Tasks 3-9
    evals/eval-<case>.yaml                 # Create — Tasks 3-9
    examples/strong-example.md             # Create — flagship skills only (Tasks 3, 6)
    examples/weak-example.md               # Create — flagship skills only (Tasks 3, 6)
  <new-skill>/
    SKILL.md                               # Create — Blocks F-J
    references/*.md                        # Create where a skill needs a durable framework doc split out
    evals/eval-*.yaml                       # Create — at least 1 per new skill
  README.md                                # Modify — catalog table, Task 22
  competencies.yaml                        # Create — Task 10, machine-readable skill↔competency map
examples/
  demo-chain/                              # Task 21 — end-to-end artifact chain
    01-transcripts.md ... 05-alignment-brief.md
CHANGELOG.md                               # Create — Task 23
README.md                                  # Modify — Task 22 (root)
```

---

## Block A — Anchor the Spec and Audit the Gap

### Task 0: Version the vision doc

**Files:**
- Create: `docs/vision/product-leadership-skills-vision.md`

**Interfaces:**
- Produces: a stable repo-relative path every later task can cite instead of "the attached file."

- [ ] **Step 1:** Save the full text of the attached `05-product-leadership-skills.md` doc verbatim to `docs/vision/product-leadership-skills-vision.md`. Fix the mangled characters visible in the source (`â` artifacts from an encoding issue, e.g. in "broader than âprompt libraryâ" and the arrow diagrams) to plain ASCII (`"prompt library"`, `->`).
- [ ] **Step 2:** Add one line at the top: `> Canonical vision doc for this repo's skill library. Referenced by docs/superpowers/plans/2026-08-23-product-leadership-skills-expansion.md.`
- [ ] **Step 3:** Commit.
  ```bash
  git add docs/vision/product-leadership-skills-vision.md
  git commit -m "docs: version the skills-library vision doc"
  ```

### Task 1: Gap-map current repo against the spec

**Files:**
- Create: `docs/skills-gap-audit.md`

**Interfaces:**
- Consumes: `docs/vision/product-leadership-skills-vision.md` (Task 0), current contents of `skills/*/SKILL.md`.
- Produces: the prioritized backlog that Blocks F-J execute from — later tasks should cite row IDs from this file rather than re-deriving the list.

- [ ] **Step 1:** Build a contract-coverage table with one row per existing skill (`synthesize-research`, `user-research`, `write-feature-spec`, `stakeholder-alignment-brief`, `prep-competency-review`, `build-dashboard`, `data-visualization`) and one column per contract element (Purpose, Trigger, Inputs, Missing-input behavior, Process, Constraints, Output, Review, Evaluation, `references/`, `examples/`, `evals/`). Mark ✅ / ❌ / ⚠️ (partial) per cell by re-reading each SKILL.md.
- [ ] **Step 2:** Build a catalog-coverage table: one row per skill named in the vision doc's seven "Core skill groups" (Discovery & research, Product definition, Prioritization & decision support, Stakeholder work, Analytics, Leadership, AI-native product workflows). Columns: `Exists in repo?`, `Repo skill name (if any)`, `Status` (built / Wave 1 backlog / later backlog — cross-reference Blocks F-J and the backlog table in Block K).
- [ ] **Step 3:** Add a short "Findings" section: which contract elements are most commonly missing (expect: Missing-input-behavior, explicit Constraints section, evals/, examples/ are the gaps — confirm by inspection rather than assuming), and which skill groups have zero coverage today (expect: AI-native product workflows, most of Analytics).
- [ ] **Step 4:** Commit.
  ```bash
  git add docs/skills-gap-audit.md
  git commit -m "docs: audit existing skills against the skill-contract and catalog"
  ```

---

## Block B — Standardize the Contract Template

### Task 2: Write the skill template and contributor guide

**Files:**
- Create: `skills/_TEMPLATE/SKILL.md`
- Create: `skills/CONTRIBUTING.md`

**Interfaces:**
- Produces: `skills/_TEMPLATE/SKILL.md` is the starting point every task in Blocks F-J copies. `skills/CONTRIBUTING.md` is what Task 22's README links to for "how to add a skill."

- [ ] **Step 1:** Write `skills/_TEMPLATE/SKILL.md` with:
  - Frontmatter stub: `name`, `description` (must state trigger conditions inline, matching the style in `skills/synthesize-research/SKILL.md:3` — not just a topic label), `argument-hint`.
  - Section skeleton with one sentence of guidance under each heading, mapped 1:1 to the contract: `## Usage`, `## Competency Connection` (cite category + sub-competency from `docs/pm-competency-model.md`), `## Required Inputs`, `## If Inputs Are Missing` (explicit fallback behavior — ask vs. proceed with caveats vs. refuse), `## Process` (numbered), `## Constraints` (what the skill must not do — every skill needs at least one, not just the flagship ones), `## Output Format`, `## Review Checkpoints` (what a human must approve before the output is used), `## Common Mistakes`, `## Practice Questions`, `## Improvement Loop`.
  - A comment block at the very top: `<!-- sourcing: adapted-from-<url> | drafted-fresh -->` per the Global Constraints sourcing-transparency rule.
- [ ] **Step 2:** Write `skills/CONTRIBUTING.md` covering, each as its own section, drawn directly from the vision doc so nothing is invented: Skill anatomy (when to add `references/`, `examples/`, `evals/` vs. keep a flat SKILL.md), Source hierarchy (approved decision > canonical docs > current customer evidence > meeting notes > working drafts > agent inference — instruct skill authors to bake this into any skill that cites multiple context sources), Context rules (a skill states the *minimum* context it needs; never "read everything"), Human judgment boundaries (the Agent-can-do / Human-should-own lists from the vision doc, reproduced verbatim so authors don't have to dig it out of the vision file), the sourcing-first rule for new skills with a link forward to Block E's Search Procedure.
- [ ] **Step 3:** Self-check: reread `docs/vision/product-leadership-skills-vision.md`'s "Skill contract," "Human judgment boundaries," "Context rules," and "Source hierarchy" sections side-by-side with the new files and confirm nothing was paraphrased incorrectly.
- [ ] **Step 4:** Commit.
  ```bash
  git add skills/_TEMPLATE/SKILL.md skills/CONTRIBUTING.md
  git commit -m "docs: add skill contract template and contributor guide"
  ```

---

## Block C — Retrofit the 7 Existing Skills

Apply this identical procedure to each skill below. Steps are shared; parameters differ per task.

**Shared per-skill procedure:**
1. Reread the skill's current SKILL.md against `docs/skills-gap-audit.md`'s per-skill row.
2. Add whichever contract sections were marked ❌/⚠️ — most commonly this means adding an explicit `## Constraints` section (what the skill must refuse or flag rather than do) and an `## If Inputs Are Missing` section (what to ask vs. what to proceed with and flag as an assumption) if not already present in substance. Do not restructure sections that already work; this is gap-filling, not a rewrite.
3. Add `evals/` with at least 2 YAML eval cases in the shape shown in the vision doc's "Example eval record" (skill, case, expected — as a list of boolean-checkable behaviors, not vague quality adjectives).
4. Commit.

### Task 3: Retrofit `synthesize-research` (flagship — also gets golden examples)

**Files:**
- Modify: `skills/synthesize-research/SKILL.md`
- Create: `skills/synthesize-research/evals/eval-contradictory-sources.yaml`
- Create: `skills/synthesize-research/evals/eval-single-weak-source.yaml`
- Create: `skills/synthesize-research/examples/strong-example.md`
- Create: `skills/synthesize-research/examples/weak-example.md`

- [ ] **Step 1-2:** Apply the shared procedure. This skill already has strong implicit constraints (`skills/synthesize-research/SKILL.md:321-329` "Tips") — promote the most load-bearing ones ("do not force findings into a predetermined narrative," "resist synthesizing more than 5-8 strong findings") into an explicit `## Constraints` heading rather than leaving them as an easy-to-skip "Tips" list at the bottom.
- [ ] **Step 3a:** `evals/eval-contradictory-sources.yaml`:
  ```yaml
  skill: synthesize-research
  case: contradictory-sources
  input_summary: >
    5 interviews say onboarding is confusing; 200-response survey NPS
    breakdown shows no onboarding complaints in write-ins.
  expected:
    - surfaces_the_contradiction_explicitly
    - does_not_silently_pick_one_source
    - checks_whether_different_populations_were_sampled
    - confidence_level_marked_low_or_medium_not_high
  ```
- [ ] **Step 3b:** `evals/eval-single-weak-source.yaml`:
  ```yaml
  skill: synthesize-research
  case: single-weak-source
  input_summary: 2 customer interviews only, no survey or usage data.
  expected:
    - does_not_present_findings_as_high_confidence
    - labels_findings_as_hypotheses_not_conclusions
    - suggests_follow_up_research_to_increase_sample
    - still_produces_full_synthesis_structure
  ```
- [ ] **Step 4:** Write `examples/strong-example.md`: a short (under one page) synthesis output that hits every eval expectation above — correct confidence labeling, attributed quotes, an explicit contradiction called out. Write `examples/weak-example.md`: the same input synthesized badly (averages reported without distribution, a "high confidence" claim from 2 interviews, no source attribution). Add 3-5 bullet points under a `## Why this is weak` heading in the weak example pointing at the specific violated rule.
- [ ] **Step 5:** Commit.
  ```bash
  git add skills/synthesize-research
  git commit -m "feat(skills): add evals and golden examples to synthesize-research"
  ```

### Task 4: Retrofit `user-research`

**Files:**
- Modify: `skills/user-research/SKILL.md`
- Create: `skills/user-research/evals/eval-missing-research-goal.yaml`
- Create: `skills/user-research/evals/eval-leading-questions.yaml`

- [ ] Apply the shared procedure (Steps 1-2). Focus: does the skill currently say what to do when the user hasn't stated a research goal or target participant profile? Add an `## If Inputs Are Missing` section if not.
- [ ] `evals/eval-missing-research-goal.yaml` — expected: `asks_for_the_decision_this_research_will_inform`, `does_not_generate_a_study_plan_from_a_vague_topic_alone`.
- [ ] `evals/eval-leading-questions.yaml` — expected: `flags_or_rewrites_leading_questions_in_a_draft_discussion_guide`, `explains_why_the_question_is_leading`.
- [ ] Commit: `git commit -m "feat(skills): add evals to user-research"`.

### Task 5: Retrofit `write-feature-spec` (flagship — also gets golden examples)

**Files:**
- Modify: `skills/write-feature-spec/SKILL.md`
- Create: `skills/write-feature-spec/evals/eval-missing-analytics-context.yaml` (this exact case is already specified in the vision doc's "Example eval record" — implement it precisely as written there)
- Create: `skills/write-feature-spec/evals/eval-unresolved-ambiguity.yaml`
- Create: `skills/write-feature-spec/examples/strong-example.md`
- Create: `skills/write-feature-spec/examples/weak-example.md`

- [ ] Apply the shared procedure.
- [ ] `evals/eval-missing-analytics-context.yaml`:
  ```yaml
  skill: write-feature-spec
  case: missing-analytics-context
  expected:
    - does_not_invent_metrics
    - identifies_missing_measurement
    - still_generates_valid_spec_structure
  ```
- [ ] `evals/eval-unresolved-ambiguity.yaml` — expected: `lists_open_questions_explicitly_rather_than_guessing_intent`, `does_not_silently_narrow_scope_to_resolve_ambiguity`.
- [ ] Golden examples: strong = a spec that lists 2-3 real open questions and marks a metric as "not yet instrumented" instead of inventing a number; weak = a spec that fabricates a specific conversion percentage and resolves an ambiguous requirement without flagging it.
- [ ] Commit: `git commit -m "feat(skills): add evals and golden examples to write-feature-spec"`.

### Task 6: Retrofit `stakeholder-alignment-brief`

**Files:**
- Modify: `skills/stakeholder-alignment-brief/SKILL.md`
- Create: `skills/stakeholder-alignment-brief/evals/eval-single-option-presented.yaml`
- Create: `skills/stakeholder-alignment-brief/evals/eval-no-recommendation-basis.yaml`

- [ ] Apply the shared procedure. The vision doc explicitly says this skill "should optimize for decision quality, not presentation volume" — check the current SKILL.md states this as a constraint, not just an aspiration in prose, and promote it to `## Constraints` if it isn't already explicit.
- [ ] `evals/eval-single-option-presented.yaml` — expected: `flags_when_only_one_option_was_given_and_asks_for_a_real_alternative_or_a_status_quo_baseline`.
- [ ] `evals/eval-no-recommendation-basis.yaml` — expected: `recommendation_is_traceable_to_specific_tradeoffs_listed_above_it`, `does_not_recommend_without_stating_the_deciding_factor`.
- [ ] Commit: `git commit -m "feat(skills): add evals to stakeholder-alignment-brief"`.

### Task 7: Retrofit `prep-competency-review`

**Files:**
- Modify: `skills/prep-competency-review/SKILL.md`
- Create: `skills/prep-competency-review/evals/eval-no-evidence-for-category.yaml`
- Create: `skills/prep-competency-review/evals/eval-hiring-review-mismatch.yaml`

- [ ] Apply the shared procedure — this skill is already close to the full contract (see `skills/prep-competency-review/SKILL.md:102-107` "Common Mistakes"); mainly needs `evals/`.
- [ ] `evals/eval-no-evidence-for-category.yaml` — expected: `absence_of_evidence_noted_as_a_gap_not_silently_omitted`, `does_not_infer_a_rating_from_general_reputation`.
- [ ] `evals/eval-hiring-review-mismatch.yaml` — expected: `flags_when_an_interview_question_tests_something_no_review_criterion_measures`, `does_not_silently_pick_one_standard`.
- [ ] Commit: `git commit -m "feat(skills): add evals to prep-competency-review"`.

### Task 8: Retrofit `build-dashboard`

**Files:**
- Modify: `skills/build-dashboard/SKILL.md`
- Create: `skills/build-dashboard/evals/eval-vanity-metric-requested.yaml`

- [ ] Apply the shared procedure. Check specifically whether the skill has a rule against building a dashboard around a vanity metric without at least flagging it — add one under `## Constraints` if missing.
- [ ] `evals/eval-vanity-metric-requested.yaml` — expected: `flags_vanity_metrics_rather_than_building_silently`, `asks_what_decision_the_dashboard_supports`.
- [ ] Commit: `git commit -m "feat(skills): add evals to build-dashboard"`.

### Task 9: Retrofit `data-visualization`

**Files:**
- Modify: `skills/data-visualization/SKILL.md`
- Create: `skills/data-visualization/evals/eval-misleading-axis.yaml`

- [ ] Apply the shared procedure.
- [ ] `evals/eval-misleading-axis.yaml` — expected: `does_not_produce_a_truncated_y_axis_without_flagging_it`, `chart_type_matches_the_claim_being_made`.
- [ ] Commit: `git commit -m "feat(skills): add evals to data-visualization"`.

---

## Block D — Machine-Readable Competency Map

### Task 10: Add `skills/competencies.yaml`

**Files:**
- Create: `skills/competencies.yaml`
- Modify: `skills/README.md` (add one line pointing to it)

**Interfaces:**
- Produces: a single structured file later tooling (or a future `team-skill-gap-analysis` skill, see Block K backlog) can parse instead of scraping prose competency-connection sections out of every SKILL.md.

- [x] **Step 1:** For every skill that exists after Block C, write one entry in the exact shape shown in the vision doc:
  ```yaml
  - skill: synthesize-research
    competencies:
      - customer-insight.voice-of-the-customer
      - customer-insight.fluency-with-data
  ```
  Use `category.sub-competency` slugs derived from the four categories / twelve sub-competencies already named in `docs/pm-competency-model.md` and already used in prose in `skills/README.md`'s table — do not invent new slugs, just slugify the existing names consistently (kebab-case, category prefix).
- [x] **Step 2:** Cross-check every entry against the prose "Competency Connection" section in the corresponding SKILL.md — they must agree; if they don't, fix the SKILL.md (it's the source of truth for humans) and this file together.
- [x] **Step 3:** Add one line to `skills/README.md`: "Machine-readable version: [skills/competencies.yaml](competencies.yaml)."
- [x] **Step 4:** Commit.
  ```bash
  git add skills/competencies.yaml skills/README.md
  git commit -m "feat(skills): add machine-readable skill-to-competency map"
  ```

---

## Block E — New-Skill Sourcing Procedure (used by every task in Blocks F-J)

### Task 11: Write the search-first procedure once, reuse it everywhere

**Files:**
- Modify: `skills/CONTRIBUTING.md` (append this section — it belongs with the other authoring guidance from Task 2)

- [ ] **Step 1:** Add a `## Sourcing a new skill` section to `skills/CONTRIBUTING.md` with this exact procedure, so Blocks F-J can reference it by name instead of repeating it:
  1. **Search first.** For the skill's stated purpose, search: (a) Anthropic's official Claude skill examples (anthropic-cookbook / anthropic-quickstarts / any published Claude "Agent Skills" example repos), (b) community lists such as "awesome-claude-skills" / "awesome-claude-code" on GitHub, (c) general GitHub/web search for `"<skill purpose>" claude skill` or `"<skill purpose>" prompt template product management`. Use WebSearch/WebFetch for this — do not rely on memory of what might exist.
  2. **Evaluate candidates against this repo's bar**, not against how polished they look: does the candidate specify inputs, missing-input behavior, constraints, and output structure? Does it avoid turning weak evidence into strong claims? Most generic prompt-library hits will fail this bar — that's expected and is itself useful signal that hand-authoring is warranted.
  3. **If a usable candidate exists:** adapt it — rewrite to this repo's SKILL.md contract and frontmatter shape, add the competency connection, add constraints/missing-input-behavior if the source lacked them, and record `<!-- sourcing: adapted-from-<url> -->` at the top of the file.
  4. **If nothing suitable is found:** draft from scratch using `skills/_TEMPLATE/SKILL.md`, using `synthesize-research` or `prep-competency-review` as style references (they are the most complete existing skills), and record `<!-- sourcing: drafted-fresh -->`.
  5. **Either way:** the skill still needs its own `evals/` (at least 1 case, 2+ preferred) before the task is done — sourcing an example does not exempt a skill from evaluation.
- [ ] **Step 2:** Commit.
  ```bash
  git add skills/CONTRIBUTING.md
  git commit -m "docs: document the search-first procedure for new skills"
  ```

**Per-skill task shape used in Blocks F-J below** (stated once, applied with each skill's parameters):
1. Run the Sourcing Procedure (Task 11) for this skill's stated purpose.
2. Create `skills/<name>/SKILL.md` with the given Purpose/Trigger, the given Required Inputs, an `## If Inputs Are Missing` section, the given Process outline turned into concrete numbered steps, the given Constraints, the given Output Format section headers, a Competency Connection section using the given competency tag(s), Common Mistakes, Practice Questions, and an Improvement Loop (mirroring the existing 7 skills' closing sections).
3. Create at least one `skills/<name>/evals/eval-<case>.yaml` per the given eval case.
4. Add a row for the skill to `skills/README.md`'s catalog table (this can be batched into Task 22 instead of repeated 15 times, see note there).
5. Commit.

---

## Block F — Wave 1 New Skills: Discovery & Definition

### Task 12: `opportunity-framing`

- **Purpose:** Turn a synthesized research finding (or a raw signal) into a framed opportunity statement with a clear "who / problem / why now."
- **Trigger:** After `synthesize-research` produces findings, or when a stakeholder hands over a raw signal ("support tickets are up 20% on X") that hasn't been framed as an opportunity yet.
- **Required inputs:** a finding or signal; who is affected; what evidence exists.
- **If inputs are missing:** if there's no evidence at all (pure opinion/HiPPO input), the skill must say so explicitly and downgrade the framing to "unvalidated hypothesis," not silently produce a confident opportunity statement.
- **Competency tag(s):** `customer-insight.voice-of-the-customer`, `product-strategy.strategic-impact`.
- **Output sections:** Opportunity statement, Who is affected + size, Evidence (with source), Why now, What's NOT the opportunity (explicit non-scope), Confidence level, Suggested next step (validate further vs. proceed to `write-intent`).
- **Eval case:** `eval-opinion-only-input.yaml` — expected: `labels_output_as_unvalidated_hypothesis`, `does_not_invent_a_sizing_number`.

### Task 13: `problem-validation`

- **Purpose:** Given a stated problem/opportunity, design and run a lightweight check (desk research prompts, targeted questions, a smoke test plan) for whether it's real before committing roadmap time.
- **Trigger:** Before committing an opportunity to a roadmap slot.
- **Required inputs:** the problem statement; existing evidence quality (from `opportunity-framing` if available).
- **If inputs are missing:** if no evidence at all exists, produce a validation plan (what to go find out), not a validation verdict.
- **Competency tag(s):** `customer-insight.fluency-with-data`, `product-strategy.business-outcome-ownership`.
- **Output sections:** Problem restated, Current evidence strength, Validation questions to answer, Cheapest way to answer each, Go/no-go criteria (stated in advance, before results come in), Recommendation only if evidence already exists.
- **Eval case:** `eval-no-existing-evidence.yaml` — expected: `produces_a_plan_not_a_verdict`, `go_no_go_criteria_defined_before_any_data_is_referenced`.

### Task 14: `write-intent`

- **Purpose:** Convert a validated opportunity into a short, approvable "product intent" doc — the input `write-feature-spec` already expects ("approved product intent" per `skills/write-feature-spec/SKILL.md`'s stated inputs) but that this repo currently has no skill to produce.
- **Trigger:** After an opportunity is framed/validated and before spec work starts.
- **Required inputs:** opportunity statement, evidence, any known constraints.
- **If inputs are missing:** if the opportunity hasn't gone through `opportunity-framing` or `problem-validation`, ask for at least the evidence and affected-user info rather than fabricating rationale.
- **Competency tag(s):** `product-strategy.product-vision-roadmapping`, `product-execution.feature-specification`.
- **Output sections:** Intent statement (one paragraph), Why this / why now, Success looks like (qualitative, pre-metrics), Explicit non-goals, Known constraints, Open strategic questions, Approval needed from (who).
- **Eval case:** `eval-vague-success-criteria.yaml` — expected: `pushes_back_on_unmeasurable_success_language`, `separates_non_goals_from_open_questions`.

### Task 15: `define-success-metrics`

- **Purpose:** Take an intent or spec and define the specific, instrumented metrics that will judge it — filling the gap the existing `write-feature-spec` eval case (`eval-missing-analytics-context`) explicitly anticipates.
- **Trigger:** During spec-writing, or when a spec was written without real metrics and needs them retrofitted.
- **Required inputs:** the intent/spec; what's currently instrumented vs. not.
- **If inputs are missing:** if instrumentation state is unknown, the output must list "instrument this before launch" items rather than assuming data will exist.
- **Competency tag(s):** `customer-insight.fluency-with-data`, `product-strategy.business-outcome-ownership`.
- **Output sections:** Primary metric (one, with target and timeframe), Guardrail metrics, Leading indicators, Metrics NOT chosen and why, Instrumentation gaps, Review checkpoint (who signs off the target is realistic).
- **Eval case:** `eval-no-instrumentation.yaml` — expected: `does_not_invent_a_baseline_number`, `flags_instrumentation_as_a_launch_blocker_not_an_afterthought`.

### Task 16: `identify-product-risks`

- **Purpose:** Systematically surface risks (technical, market, UX, compliance, adoption) in a spec or plan before it ships.
- **Trigger:** Spec review, pre-launch, or when a stakeholder asks "what could go wrong."
- **Required inputs:** the spec/plan; known constraints; compliance context if any.
- **If inputs are missing:** if compliance/legal context is unknown, flag it as an open risk category rather than skipping it silently.
- **Competency tag(s):** `product-execution.product-quality`, `product-strategy.strategic-impact`.
- **Output sections:** Risk register table (risk / likelihood / impact / category / mitigation / owner), Risks explicitly out of scope for this pass and why, Top 3 by (likelihood × impact).
- **Eval case:** `eval-unknown-compliance-context.yaml` — expected: `flags_missing_compliance_review_as_a_risk_not_a_silent_gap`.

---

## Block G — Wave 1 New Skills: Prioritization & Decision Support

### Task 17: `write-decision-brief`

- **Purpose:** General-purpose decision brief for any product decision (not just stakeholder-facing ones) — options, trade-offs, recommendation, what's needed to decide.
- **Trigger:** Any time a decision needs to be written down before it's made, distinct from `stakeholder-alignment-brief` which is specifically a pre-read *for a meeting with stakeholders*.
- **Required inputs:** the decision to make; at least one real alternative (see Constraint below); constraints.
- **If inputs are missing:** if only one option is given, this skill (like `stakeholder-alignment-brief`, per Task 6) must ask for a genuine alternative or an explicit status-quo baseline before proceeding.
- **Competency tag(s):** `product-strategy.strategic-impact`, `influencing-people.stakeholder-management`.
- **Output sections:** mirror the vision doc's shown template exactly — Decision / Why now / Current state / Options / Trade-offs / Recommendation / Risks / Decision needed.
- **Eval case:** `eval-single-option.yaml` — expected: `requests_a_real_alternative_or_explicit_status_quo_before_producing_a_recommendation`.

### Task 18: `compare-options`

- **Purpose:** Structured side-by-side comparison of 2+ options against explicit criteria — a reusable building block `write-decision-brief` and `roadmap-tradeoff-analysis` (backlog) can both call on.
- **Trigger:** Any time 2+ concrete options need to be scored against the same criteria.
- **Required inputs:** the options; the criteria (or a request to help define them).
- **If inputs are missing:** if no criteria are given, the skill must propose criteria and get them confirmed before scoring — never silently pick its own weighting.
- **Competency tag(s):** `product-strategy.strategic-impact`, `customer-insight.fluency-with-data`.
- **Output sections:** Criteria (with weights if applicable, explicitly confirmed), Scoring table, Where options tie and why that matters, Sensitivity note (does the ranking change if a criterion's weight shifts).
- **Eval case:** `eval-no-criteria-given.yaml` — expected: `proposes_criteria_for_confirmation_rather_than_assuming`.

### Task 19: `prepare-prioritization`

- **Purpose:** Take a backlog of candidate items and structure them for a prioritization session (RICE/ICE-style scoring plus qualitative flags), without making the prioritization call itself.
- **Trigger:** Before a roadmap/backlog prioritization meeting.
- **Required inputs:** the candidate list; a scoring framework preference (or default to asking).
- **If inputs are missing:** if impact/effort estimates are missing for an item, mark that item's score as "insufficient data" rather than guessing a number to keep the table complete.
- **Competency tag(s):** `product-strategy.business-outcome-ownership`, `product-execution.product-delivery`.
- **Output sections:** Scoring table per item, Items with insufficient data (flagged, not scored), Qualitative flags (strategic bets, technical debt, compliance-mandated — items that shouldn't be pure-score-ranked), Explicit note that the human makes the final call.
- **Eval case:** `eval-missing-effort-estimate.yaml` — expected: `marks_item_as_insufficient_data_rather_than_guessing`, `does_not_present_the_ranking_as_the_decision_itself`.

---

## Block H — Wave 1 New Skills: Stakeholder & Leadership

### Task 20: `executive-update`

- **Purpose:** Turn project/product status into a concise executive-level update (progress, risks, asks) distinct from a full stakeholder alignment brief.
- **Trigger:** Recurring exec/board update, or ad hoc "what's the state of X" request.
- **Required inputs:** current status, key metrics, blockers, what's being asked of the exec (if anything).
- **If inputs are missing:** if no explicit ask exists, say so rather than manufacturing one — not every update needs a decision from the reader.
- **Competency tag(s):** `influencing-people.managing-up`, `product-strategy.business-outcome-ownership`.
- **Output sections:** Headline (one sentence), Progress vs. plan, Key metric movement, Risks/blockers, Ask (or "no ask this cycle"), Appendix pointer (link to fuller detail, not inlined).
- **Eval case:** `eval-no-ask-this-cycle.yaml` — expected: `explicitly_states_no_ask_rather_than_inventing_one`.

### Task 21: `decision-log`

- **Purpose:** Maintain/append a running log of product decisions (what was decided, why, by whom, what would change the decision) as a durable artifact — this is the "canonical decision" top of the vision doc's Source Hierarchy, which today has no skill that produces it.
- **Trigger:** After any decision brief is approved, or when asked "what did we decide about X and why."
- **Required inputs:** the decision; the rationale; date; decision-maker.
- **If inputs are missing:** never log a decision without a stated rationale — ask for it rather than inferring one from context.
- **Competency tag(s):** `influencing-people.stakeholder-management`, `product-strategy.strategic-impact`.
- **Output sections:** append-only entry format (Date / Decision / Rationale / Decided by / Reversibility trigger — what would cause revisiting), plus, when asked to query the log: a lookup that surfaces prior entries relevant to a new question.
- **Eval case:** `eval-no-rationale-given.yaml` — expected: `refuses_to_log_a_decision_with_no_stated_rationale`.

---

## Block I — Wave 1 New Skills: Analytics

### Task 22: `metric-definition`

- **Purpose:** Produce a rigorous metric definition doc (exact calculation, edge cases, owner) — a prerequisite `build-dashboard` and `define-success-metrics` both implicitly assume exists.
- **Trigger:** Before building a dashboard, or when two people disagree on how a metric is calculated.
- **Required inputs:** the metric name/intent; data source availability.
- **If inputs are missing:** if the data source can't actually support the definition as stated, say so rather than defining an uncomputable metric.
- **Competency tag(s):** `customer-insight.fluency-with-data`.
- **Output sections:** Metric name, Exact formula, Edge cases (e.g., how are refunds/test accounts handled), Data source, Refresh cadence, Owner, Known limitations.
- **Eval case:** `eval-uncomputable-from-stated-source.yaml` — expected: `flags_that_the_data_source_cannot_support_the_requested_definition`.

### Task 23: `experiment-analysis`

- **Purpose:** Analyze an A/B or experiment result and produce a read that respects statistical validity — filling the gap next to `generate-experiment-plan` (backlog) with the analysis half of that lifecycle.
- **Trigger:** After an experiment concludes.
- **Required inputs:** sample sizes, effect size, confidence/significance data, run duration.
- **If inputs are missing:** if significance data isn't provided, the skill must refuse to declare a winner — it can describe the observed difference but must label it as not yet statistically validated.
- **Competency tag(s):** `customer-insight.fluency-with-data`, `product-strategy.business-outcome-ownership`.
- **Output sections:** Result summary, Statistical validity check (sample size, duration, significance), Practical significance (is the effect big enough to matter even if significant), Segment splits if available, Recommendation (ship / kill / extend / inconclusive), Caveats.
- **Eval case:** `eval-no-significance-data.yaml` — expected: `refuses_to_declare_a_winner_without_significance_data`, `still_describes_the_observed_difference`.

---

## Block J — AI-Native Product Workflows (repo differentiator)

These directly implement the vision doc's "Suggested high-value new skills" section and its explicit claim that they'd "strongly support hands-on AI product leadership positioning" — prioritize sourcing search here especially hard, since this is a newer skill category and public examples (from Anthropic's own published safety/eval guidance) are more likely to exist than for generic PM templates.

### Task 24: `context-audit`

- **Purpose:** Check a product workflow/knowledge base for stale context, duplicate definitions, missing canonical sources, and contradictory decisions.
- **Trigger:** Periodically, or before onboarding an agent workflow onto a knowledge base.
- **Required inputs:** the set of docs/sources to audit.
- **If inputs are missing:** if no canonical source is designated for a topic, flag that as the finding itself rather than picking one.
- **Competency tag(s):** `customer-insight.fluency-with-data`, `product-execution.product-quality`.
- **Output sections:** Stale context found, Duplicate/conflicting definitions, Missing canonical sources, Contradictory decisions (cite both), Recommended source-of-truth designations (for human approval).
- **Eval case:** `eval-two-conflicting-docs.yaml` — expected: `cites_both_conflicting_sources_explicitly`, `does_not_silently_prefer_the_more_recent_one_without_saying_so`.

### Task 25: `agent-readiness-review`

- **Purpose:** Assess whether a given product workflow is actually suitable for agent automation before it's handed off.
- **Trigger:** Before automating a workflow with an agent.
- **Required inputs:** the workflow description; failure cost if the agent gets it wrong; reversibility of its actions.
- **If inputs are missing:** if reversibility/failure-cost is unstated, treat that as a blocking unknown, not a low-risk default.
- **Competency tag(s):** `product-strategy.strategic-impact`, `product-execution.product-quality`.
- **Output sections:** Workflow summary, Reversibility of actions, Failure cost if wrong, Required human checkpoints, Readiness verdict (ready / ready-with-guardrails / not-ready), Guardrails needed if not fully ready.
- **Eval case:** `eval-unstated-reversibility.yaml` — expected: `treats_unstated_reversibility_as_blocking_not_as_low_risk`.

### Task 26: `AI-feature-risk-review`

- **Purpose:** Check an AI-powered feature for user harm, incorrect-action risk, data exposure, permission boundaries, and failure recovery — using exactly the five checks named in the vision doc.
- **Trigger:** Before shipping an AI-powered feature.
- **Required inputs:** feature description; what actions the AI can take autonomously vs. with approval; data it can access.
- **If inputs are missing:** if the autonomy boundary (what the AI can do without approval) isn't specified, this is itself the top risk finding — surface it first, don't bury it.
- **Competency tag(s):** `product-execution.product-quality`, `product-strategy.strategic-impact`.
- **Output sections:** User harm scenarios, Incorrect-action risk (what happens if the model is wrong), Data exposure, Permission boundaries, Failure recovery (what happens when it fails), Overall risk rating with rationale.
- **Eval case:** `eval-unstated-autonomy-boundary.yaml` — expected: `surfaces_unstated_autonomy_boundary_as_the_top_finding`.

### Task 27: `eval-plan`

- **Purpose:** Turn an AI feature's expected behavior into measurable test cases — literally the practice this whole plan uses for its own skills (Blocks C, F-J eval cases), turned into a reusable skill.
- **Trigger:** When defining how an AI feature's quality will be measured before/after launch.
- **Required inputs:** the feature's expected behaviors; known failure modes if any.
- **If inputs are missing:** if failure modes aren't known yet, the skill should still produce cases for the stated expected behaviors and explicitly list "failure modes to be identified" as an open item, rather than blocking entirely.
- **Competency tag(s):** `product-execution.product-quality`, `customer-insight.fluency-with-data`.
- **Output sections:** Eval cases (mirroring the exact `skill/case/expected` YAML shape used throughout this plan), Coverage gaps (behaviors with no case yet), Suggested cadence (pre-launch only vs. ongoing regression).
- **Eval case (of the eval-plan skill itself):** `eval-no-known-failure-modes.yaml` — expected: `still_produces_cases_for_stated_behaviors`, `explicitly_lists_failure_modes_as_open_rather_than_skipping_the_section`.

### Task 28: `human-in-the-loop-design`

- **Purpose:** Identify which steps of an agent workflow should be autonomous, reviewed, approved, or blocked.
- **Trigger:** Designing or auditing an agent-driven workflow.
- **Required inputs:** the workflow's steps; the cost/reversibility of each step's actions (can reuse output from `agent-readiness-review` if available).
- **If inputs are missing:** default any step with unknown reversibility to "approval required," never to "autonomous."
- **Competency tag(s):** `product-strategy.strategic-impact`, `product-execution.product-quality`.
- **Output sections:** Step-by-step table (step / autonomous-review-approval-blocked / rationale), Escalation path for blocked steps, What changes the classification later (e.g., after N successful reviewed runs).
- **Eval case:** `eval-unknown-reversibility-step.yaml` — expected: `defaults_unknown_reversibility_steps_to_approval_required_not_autonomous`.

---

## Block K — Demo Chain and Backlog Tracking

### Task 29: Build the end-to-end demo chain

**Files:**
- Create: `examples/demo-chain/README.md`
- Create: `examples/demo-chain/01-transcripts.md`
- Create: `examples/demo-chain/02-research-synthesis.md`
- Create: `examples/demo-chain/03-opportunity-framing.md`
- Create: `examples/demo-chain/04-intent.md`
- Create: `examples/demo-chain/05-feature-spec.md`
- Create: `examples/demo-chain/06-alignment-brief.md`

**Interfaces:**
- Consumes: `synthesize-research`, `opportunity-framing` (Task 12), `write-intent` (Task 14), `write-feature-spec`, `stakeholder-alignment-brief` — must be executed after Block F.

- [ ] **Step 1:** Write a small, plausible, fictional set of 3-4 "customer interview transcripts" in `01-transcripts.md` (a few paragraphs each) about one coherent problem area, so the chain has a believable throughline.
- [ ] **Step 2:** Actually run each skill in sequence against the prior file's output (not hand-waved — invoke `synthesize-research` on file 1, `opportunity-framing` on file 2's output, etc.) and save each real output as the numbered file.
- [ ] **Step 3:** Write `examples/demo-chain/README.md` explaining the chain, linking each file to the skill that produced it, and stating explicitly: "each stage's output is a durable artifact the next stage consumes" (this is the exact point the vision doc says the demo must make).
- [ ] **Step 4:** Link this demo from the root `README.md`'s "Example" section (Task 22 wires this in).
- [ ] **Step 5:** Commit.
  ```bash
  git add examples/demo-chain
  git commit -m "docs: add end-to-end demo chain from transcripts to alignment brief"
  ```

### Task 30: Record the full backlog (skills not built in Waves 1)

**Files:**
- Modify: `docs/skills-gap-audit.md` (append, don't create a new file — keep one gap-tracking source of truth)

- [ ] Add a "Backlog — not yet built" table listing every remaining vision-doc skill not covered by Tasks 12-28: `competitor-analysis`, `JTBD-synthesis`, `decompose-product-problem`, `generate-experiment-plan`, `roadmap-tradeoff-analysis`, `assumption-mapping`, `product-review-prep`, `launch-readiness-review`, `funnel-analysis`, `retention-analysis`, `interview-plan`, `PM-coaching-plan`, `team-skill-gap-analysis`, `product-org-review`, `AI-product-metrics`. For each, note the skill group and one sentence on why it wasn't in Wave 1 (either lower stated priority, or overlaps heavily with a Wave 1 skill so should be scoped only after real usage shows it's needed — this is a YAGNI call, not an oversight).
- [ ] Commit: `git commit -m "docs: record full skill backlog beyond Wave 1"`.

---

## Block L — Positioning, Catalog, Versioning

### Task 31: Rebuild the skill catalog table and root README positioning

**Files:**
- Modify: `README.md`
- Modify: `skills/README.md`

- [ ] **Step 1:** In `skills/README.md`, replace the existing table with one row per skill that exists after Blocks C+F-J (22 skills total: 7 retrofitted + 15 new), columns: `Skill | Use case | Competency`. This single step replaces the "add a row per new-skill task" note deferred from Block E.
- [ ] **Step 2:** In root `README.md`, add the vision doc's exact positioning statement as a new lead line under the title: "A reusable library of AI agent skills for product discovery, decision-making, execution, leadership, and product operations," reconciled with the existing "Repository goal" section (don't duplicate — the existing goal section is good and should stay; add the positioning line as a sharper one-sentence summary above it).
- [ ] **Step 3:** Add a "What makes it different" subsection listing exactly the five points from the vision doc's README-structure guidance: skills not prompts, evidence-based, human review points, competency mapping, evaluation.
- [ ] **Step 4:** Link `examples/demo-chain/README.md` from the README's usage section as "See a full worked example."
- [ ] **Step 5:** Commit.
  ```bash
  git add README.md skills/README.md
  git commit -m "docs: refresh positioning, catalog table, and demo link in READMEs"
  ```

### Task 32: Add versioning and changelog

**Files:**
- Create: `CHANGELOG.md`
- Modify: `.claude-plugin/plugin.json` (bump version)

- [ ] **Step 1:** Read the current `.claude-plugin/plugin.json` version field and decide the bump (this expansion adds 15 skills and restructures 7 — a minor version bump, not a patch).
- [ ] **Step 2:** Create `CHANGELOG.md` with one entry for this expansion: what changed (contract standardization, evals added, 15 new skills across Discovery/Definition/Prioritization/Stakeholder/Analytics/AI-native groups, competency map, demo chain), why (close the gap identified in `docs/skills-gap-audit.md` against the vision doc), expected behavior impact (existing 7 skills behave the same for users — this is additive plus stricter internal contract, not a breaking change).
- [ ] **Step 3:** Commit.
  ```bash
  git add CHANGELOG.md .claude-plugin/plugin.json
  git commit -m "chore: bump plugin version and add changelog for skills expansion"
  ```

---

## Block M — Final Self-Audit Against the Spec

### Task 33: Run the repository quality bar checklist

**Files:**
- Modify: `docs/skills-gap-audit.md` (append final section)

- [ ] For every skill in the repo, confirm it can answer, in writing, the 7 questions from the vision doc's "Repository quality bar": problem solved, when to use, context needed, what the agent does, what stays a human decision, how quality is checked, known failure modes. Spot-check at least 5 skills by rereading them fresh; if any question isn't answerable from the file itself, fix that file before closing this task.
- [ ] Confirm the repo overall against the "Avoid" list: not a prompt collection (every skill has process + constraints + eval, not just a prompt), not a PM-quote library, not generic templates (outputs are tied to competencies and have failure-mode-specific constraints), not a competency encyclopedia (competencies only appear where a skill exercises them), no claim anywhere that agents replace product judgment (grep for language like "the AI decides" or "automatically approve" and remove/reword any hit).
- [ ] Append a short "Closing self-audit" section to `docs/skills-gap-audit.md` recording the outcome.
- [ ] Commit.
  ```bash
  git add docs/skills-gap-audit.md
  git commit -m "docs: close out expansion with repository quality-bar self-audit"
  ```

---

## Execution Order Summary

1. **Block A** (Tasks 0-1) — spec + audit. Do first; everything else cites these files.
2. **Block B** (Task 2) — template + contributing guide.
3. **Block C** (Tasks 3-9) — retrofit existing skills. Can run in parallel with each other once Block B is done.
4. **Block D** (Task 10) — competency map. Needs Block C done (reads final SKILL.md state).
5. **Block E** (Task 11) — sourcing procedure. Needs Block B; independent of C/D.
6. **Blocks F-J** (Tasks 12-28) — new skills. Each is independent of the others; can be parallelized across subagents. Needs Block E done first.
7. **Block K** (Tasks 29-30) — demo chain (needs Block F's `opportunity-framing`/`write-intent` done) and backlog recording (needs Blocks F-J done, to know what's *not* covered).
8. **Block L** (Tasks 31-32) — README/catalog/versioning. Needs everything above done (it's the summary layer).
9. **Block M** (Task 33) — final audit. Last, always.
