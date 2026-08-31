# Product Leadership Skills

A library of Claude Code skills and reference frameworks for product leaders — turning repeatable product-management workflows into instructions an agent can execute and a human can review, evidenced against a shared competency model instead of a pile of one-off prompts.

## Problem

Product leaders repeat the same workflows constantly — writing a spec from a rough idea, synthesizing scattered research, briefing stakeholders on a decision, prepping a competency-based performance review — and mostly do it from scratch each time, in whatever shape that day's tool or mood produces. Two things are usually missing:

- **Consistency.** The same kind of output (a spec, a research synthesis, a review) looks different every time, so it's hard to reuse as evidence in a coaching conversation, a performance review, or a hiring calibration.
- **A guardrail against AI making things up.** Asking an LLM to "write me a spec" or "summarize this research" is fast, but nothing stops it from inventing a metric that was never measured or quietly resolving an ambiguous requirement instead of flagging it.

This repository is for a product leader (or a team) who wants Claude Code to help with these workflows without either problem — output that's structured the same way every time, and instructions that make the agent say "I don't have that" instead of guessing.

## Product

The repository is two things working together:

1. **`skills/`** — an installable Claude Code plugin: 9 skills, each a `SKILL.md` that Claude Code runs directly (`/write-feature-spec`, `/synthesize-research`, etc.). No custom agent code — see [docs/decisions/001](docs/decisions/001-markdown-skills-not-custom-agent-code.md).
2. **A PM competency model** (based on Ravi Mehta's model) that every skill traces back to, so skill output can double as evidence in development coaching, performance review, and hiring/interview calibration — the same competency language used across all three.

| Skill | Competency category | Sub-competencies |
| --- | --- | --- |
| [synthesize-research](skills/synthesize-research/SKILL.md) | Customer Insight | Voice of the Customer, Fluency with Data |
| [user-research](skills/user-research/SKILL.md) | Customer Insight | Voice of the Customer, Fluency with Data |
| [write-feature-spec](skills/write-feature-spec/SKILL.md) | Product Execution | Feature Specification |
| [stakeholder-alignment-brief](skills/stakeholder-alignment-brief/SKILL.md) | Influencing People | Stakeholder Management |
| [executive-update](skills/executive-update/SKILL.md) | Influencing People | Stakeholder Management |
| [decision-log](skills/decision-log/SKILL.md) | Influencing People | Stakeholder Management |
| [prep-competency-review](skills/prep-competency-review/SKILL.md) | Cross-cutting | All four categories |
| [build-dashboard](skills/build-dashboard/SKILL.md) | Product Strategy | Business Outcome Ownership, Strategic Impact |
| [data-visualization](skills/data-visualization/SKILL.md) | Support skill | Backs Fluency with Data and Strategic Impact |

Full table with descriptions: [skills/README.md](skills/README.md). Machine-readable version: [skills/competencies.yaml](skills/competencies.yaml).

## Core workflows

One skill end to end — `write-feature-spec`, turning an ambiguous request into an actionable spec ([skills/write-feature-spec/SKILL.md](skills/write-feature-spec/SKILL.md)):

```text
1. Clarify the input — what triggered this, who it's for, what trade-off
   is still open, whether it's backed by research or just a hunch.
2. If a required input is missing, say so explicitly instead of guessing:
   - no research backing it → state that it's a hunch, don't present it as validated
   - instrumentation unknown → flag the missing measurement, don't invent a number
   - scope unresolved → list it under Open Questions, don't silently narrow it
3. Define scope and intent.
4. Specify behavior.
5. Define success metrics.
6. Sequence and de-risk the rollout.
   -> Output: a spec with Problem / Goals & Non-Goals / Assumptions /
      User Flow / Success Metrics / Open Questions & Risks / Rollout Plan.
```

`user-research` plans and runs a study; `synthesize-research` analyzes the results once it's done — most skills are meant to chain this way rather than run in isolation, though there is no automated demo chain yet (see Limitations).

## AI design decisions

| Decision | Choice | Why |
| --- | --- | --- |
| Execution model | Markdown `SKILL.md` run natively by Claude Code, no custom agent runtime | Instructions stay reviewable by a product leader, not just an engineer — see [ADR 001](docs/decisions/001-markdown-skills-not-custom-agent-code.md) |
| Quality mechanism | Evals as YAML case files (`skill / case / expected`), one per known failure mode | Makes "does this skill behave correctly" reproducible and inspectable, not a demo claim — see [ADR 003](docs/decisions/003-eval-driven-quality-via-yaml-cases.md) |
| Context resolution | Fixed source hierarchy: approved decision > canonical docs > current customer evidence > meeting notes > working drafts > agent inference | Several skills draw on conflicting inputs; a fixed order makes conflict resolution deterministic — see [ADR 002](docs/decisions/002-competency-model-alignment-and-source-hierarchy.md) |
| Competency grounding | Every skill maps to a PM competency sub-competency, in prose and in `competencies.yaml` | Keeps output usable as review/coaching/hiring evidence, not just a finished task — see [ADR 002](docs/decisions/002-competency-model-alignment-and-source-hierarchy.md) |
| Golden examples | Shipped for 2 of 9 skills (the flagship ones), added only once real content exists | An aspirational or empty `examples/` folder is worse than none — per `skills/CONTRIBUTING.md` |

## Human-agent boundary

**Skills do autonomously:**

- turn provided research, feedback, or context into a structured draft (spec, brief, synthesis, dashboard, review prep)
- apply the fixed source hierarchy to resolve conflicting inputs
- flag missing inputs, unvalidated assumptions, or unresolved ambiguity instead of guessing

**Always requires human review:**

- every skill produces a draft document in a chat response — no skill calls an API, writes to a system, or takes an action outside that response
- `prep-competency-review` output specifically: skills format evidence about a person's work; a human makes the judgment call, not the skill

**Not yet defined:** a full repo-wide statement of exactly where agent-assistance ends and human judgment begins is still being written — `docs/vision/product-leadership-skills-vision.md`'s "Human judgment boundaries" section is a deliberately-left placeholder (its source document wasn't available when the vision doc was drafted), rather than a guessed answer. See Limitations.

## Safety / trust model

Skills never call an external API, write to a system, or execute an action — the only "execution" is a human reading and choosing to use a Markdown draft, so there is no write-approval or policy-engine layer to build. The trust question this repo actually has to answer is *does the draft fabricate anything*, and that's handled deterministically at the skill-contract level, not by hoping the model behaves:

- every skill's `## If Inputs Are Missing` (or equivalent) section states what to do when an input is absent — ask, or flag the gap explicitly — instead of silently filling it in
- every skill has at least one eval case testing exactly this (e.g. `write-feature-spec`'s `eval-missing-analytics-context.yaml` checks the skill does not invent a metric and instead names the missing measurement)

## Evaluation

- **Eval coverage:** 9 of 9 shipped skills have at least one YAML eval case in `skills/<name>/evals/`, each testing a specific failure mode (fabricated evidence, silently-resolved ambiguity, skipped-but-unflagged missing evidence).
- **Golden examples:** 2 of 9 skills (`synthesize-research`, `write-feature-spec`) ship a strong/weak example pair in `skills/<name>/examples/`.
- **Contract coverage:** a full per-skill table (Purpose / Trigger / Inputs / Missing-input behavior / Process / Constraints / Output / Review / Evaluation) is tracked in [docs/skills-gap-audit.md](docs/skills-gap-audit.md) — that snapshot is dated 2026-08-24; eval coverage has reached 9/9 since, the rest of the table still reflects that date.
- There is no automated runner executing eval cases against a live model yet — see Limitations.

## Observability

There's no runtime to trace: a skill invocation is a single Claude Code turn producing a Markdown artifact, not a multi-step agent with tool calls to log. The reproducible record of "what does correct behavior look like" is the eval suite and, for flagship skills, the golden strong/weak example pair — not a request trace.

## Running locally

```text
/plugin marketplace add AndyMelnykov/product_leadership_skills
/plugin install product-leadership-skills@product-leadership-skills
```

Full install/verify/update/uninstall steps: [INSTALLATION.md](INSTALLATION.md).

## Repository layout

```text
README.md                    this file
LICENSE
INSTALLATION.md               plugin install/verify/update steps
.claude-plugin/               plugin.json + marketplace.json manifests
skills/                       the installable plugin — one folder per skill
  <skill-name>/SKILL.md         the skill itself
  <skill-name>/evals/           YAML eval cases (all 9 skills)
  <skill-name>/examples/        golden strong/weak pair (2 of 9 skills)
  competencies.yaml              machine-readable skill -> competency map
  CONTRIBUTING.md                 skill contract, sourcing procedure, folder rules
docs/
  pm-competency-model.md        the competency model every skill traces to
  skills-gap-audit.md            contract-coverage snapshot
  decisions/                     architecture decision records
  vision/                        canonical vision doc (partially placeholder — see Limitations)
  superpowers/plans/             tracked implementation plan for the skill expansion
Business_structure_stakeholders/  competency deep-dive: business & structure
People_culture/                   competency deep-dive: people & culture
Product_management_execution/     competency deep-dive: product execution
Strategy_thinking_storytelling/   competency deep-dive: strategy & storytelling
```

## Limitations

- **Vision doc is a placeholder skeleton.** `docs/vision/product-leadership-skills-vision.md` has several sections marked TODO (positioning statement, human judgment boundaries, decision-brief template) pending a source document that wasn't available when it was drafted. These are deliberately left blank rather than filled in with invented content — see `skills/CONTRIBUTING.md`.
- **Wave 1 skill expansion is 2 of 17 done.** `executive-update` and `decision-log` have shipped; opportunity framing, decision support (write-decision-brief, compare-options, prepare-prioritization), analytics (metric-definition, experiment-analysis), and the entire "AI-native product workflows" group (context-audit, agent-readiness-review, AI-feature-risk-review, eval-plan, human-in-the-loop-design) are scoped but not built. Full backlog: [docs/skills-gap-audit.md](docs/skills-gap-audit.md), tracked plan: `docs/superpowers/plans/2026-08-23-product-leadership-skills-expansion.md`.
- **No worked demo chain yet.** Skills are documented as chaining into each other (e.g. `user-research` -> `synthesize-research`), but there's no example showing one skill's real output feeding the next end to end.
- **Eval cases aren't automated.** They're a reviewable specification of expected behavior (`skill / case / expected`), not a CI-gated test suite run against a live model.
- **Golden examples exist for 2 of 9 skills.** The rest rely on evals and the SKILL.md's own guidance alone.
- **No versioned changelog yet.** `.claude-plugin/plugin.json` is at `1.0.0`; a `CHANGELOG.md` and version bump are planned once the Wave 1 expansion lands (see Roadmap), not before, so it reflects a real milestone rather than incremental noise.

## Roadmap

### Finish the Wave 1 skill expansion

Why: 15 of 17 scoped skills — including the entire "AI-native product workflows" group, which is this repo's most differentiated skill category — aren't built yet. Detail: [docs/skills-gap-audit.md](docs/skills-gap-audit.md).

### Worked demo chain

Why: right now every skill's example lives in isolation. Showing one skill's output feeding the next is what actually proves "workflows," not just "skills."

### CHANGELOG.md and a version bump past 1.0.0

Why: the plugin manifest hasn't moved since the initial 7-skill release; a real changelog entry lands once Wave 1 skills ship, not before.

Tracked in full: `docs/superpowers/plans/2026-08-23-product-leadership-skills-expansion.md`.

## Product decisions

| Decision | Choice | Trade-off |
| --- | --- | --- |
| Skill format | Markdown, not custom agent code | Reviewable by non-engineers, but not unit-testable — evals fill that gap |
| Competency alignment | Every skill traces to a PM competency sub-competency | Reusable as review/coaching/hiring evidence, but narrows what's "in scope" for a new skill |
| Golden examples | Only for flagship skills, only once real content exists | Honest repo state over aspirational folders, at the cost of thinner guidance for newer skills |
| Missing-input handling | Skills must state what to do when inputs are absent | Slower first output (the skill asks a question) in exchange for not fabricating evidence |
| Source hierarchy | Fixed conflict-resolution order across input types | Removes ambiguity, at the cost of a skill sometimes needing to say a source "lost" |

Full rationale: [docs/decisions/](docs/decisions/).

## PM competency model

Based on Ravi Mehta's PM competency model, used across three connected workflows: development and coaching, performance review and feedback, and hiring and interview calibration. Competencies define what good looks like, performance reviews assess evidence against them, and interviews are designed to test the same capabilities — so people get consistent expectations across all three.

- Model overview: [docs/pm-competency-model.md](docs/pm-competency-model.md)
- Visual: [docs/assets/pm-competency-model.svg](docs/assets/pm-competency-model.svg)
- Deep dives by competency area: [Business_structure_stakeholders](Business_structure_stakeholders/README.md), [People_culture](People_culture/README.md), [Product_management_execution](Product_management_execution/README.md), [Strategy_thinking_storytelling](Strategy_thinking_storytelling/README.md)

## License

[MIT](LICENSE)
