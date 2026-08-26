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

| Skill | Competency category | Sub-competencies |
| --- | --- | --- |
| [synthesize-research](synthesize-research/SKILL.md) | Customer Insight | Voice of the Customer, Fluency with Data |
| [user-research](user-research/SKILL.md) | Customer Insight | Voice of the Customer, Fluency with Data |
| [write-feature-spec](write-feature-spec/SKILL.md) | Product Execution | Feature Specification |
| [stakeholder-alignment-brief](stakeholder-alignment-brief/SKILL.md) | Influencing People | Stakeholder Management |
| [prep-competency-review](prep-competency-review/SKILL.md) | Cross-cutting | All four categories — organizes review, coaching, and interview prep around the model |
| [build-dashboard](build-dashboard/SKILL.md) | Product Strategy | Business Outcome Ownership, Strategic Impact |
| [data-visualization](data-visualization/SKILL.md) | Support skill (not directly invoked) | Backs Fluency with Data and Strategic Impact for any skill that needs a chart |

`user-research` plans and runs a study; `synthesize-research` analyzes the results once it's done — use them together. `build-dashboard` produces a stakeholder-facing artifact; `data-visualization` is the reference it (and other skills) draw on for a single chart.

Machine-readable version: [skills/competencies.yaml](competencies.yaml).

Add new skills here as the repository grows. When adding one, name it for what it produces, tie it to the specific sub-competency(ies) it exercises, and give it practice questions and an improvement loop so it stays consistent with the skills above.
