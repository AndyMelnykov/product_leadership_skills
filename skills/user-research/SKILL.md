---
name: user-research
description: Plan, conduct, and synthesize user research. Trigger with "user research plan", "interview guide", "usability test", "survey design", "research questions", or when the user needs help with any aspect of understanding their users through research.
---

# User Research

Help plan, execute, and synthesize user research studies.

## Competency Connection

This skill exercises **Voice of the Customer** and **Fluency with Data**, both under **Customer Insight** in the [PM competency model](../../../docs/pm-competency-model.md). It covers the *planning and conducting* side of research — choosing the right method, writing a guide that gets real signal, picking an honest sample size. For the *analysis* side (turning raw notes and responses into ranked findings), use the `synthesize-research` skill once the study is run.

## Required Inputs

- The decision this research will inform, or at minimum a research question.
- Who the target participants are (segment, role, or user type).

## If Inputs Are Missing

If no decision or research question is stated, ask for it before proposing a study plan — do not generate a research plan, method choice, or sample size from a vague topic alone (e.g., "let's do some user research on onboarding" is not enough to plan against). If the target participant profile is unclear, ask who the research needs to represent; a study plan for "users" in general is rarely actionable.

## Constraints

- Do not draft a leading question into a discussion guide without flagging it and explaining why it's leading (e.g., "Don't you find this confusing?" presumes an answer). Rewrite it neutrally and note the change.

## Research Methods

| Method | Best For | Sample Size | Time |
|--------|----------|-------------|------|
| User interviews | Deep understanding of needs and motivations | 5-8 | 2-4 weeks |
| Usability testing | Evaluating a specific design or flow | 5-8 | 1-2 weeks |
| Surveys | Quantifying attitudes and preferences | 100+ | 1-2 weeks |
| Card sorting | Information architecture decisions | 15-30 | 1 week |
| Diary studies | Understanding behavior over time | 10-15 | 2-8 weeks |
| A/B testing | Comparing specific design choices | Statistical significance | 1-4 weeks |

Pick the method by what decision it needs to inform, not by what's fastest to run: a roadmap bet worth quarters of engineering time deserves more than a 5-person hallway test.

## Interview Guide Structure

1. **Warm-up** (5 min): Build rapport, explain the session
2. **Context** (10 min): Understand their current workflow
3. **Deep dive** (20 min): Explore the specific topic
4. **Reaction** (10 min): Show concepts or prototypes
5. **Wrap-up** (5 min): Anything we missed? Thank them.

## Analysis Framework

- **Affinity mapping**: Group observations into themes
- **Impact/effort matrix**: Prioritize findings
- **Journey mapping**: Visualize the user experience over time
- **Jobs to be done**: Understand what users are hiring your product to do

For a full synthesis pass across multiple interviews, surveys, or feedback sources, use the `synthesize-research` skill rather than repeating this analysis manually.

## Deliverables

- Research plan (objectives, methods, timeline, participants)
- Interview guide (questions, probes, activities)
- Synthesis report (themes, insights, recommendations) — see `synthesize-research`
- Highlight reel (key quotes and observations)

## Practice Questions

- Does the chosen method match the size of the decision it's informing, or was it picked for convenience?
- Could someone else run this interview guide and get comparably useful signal, or does it depend on a specific interviewer's instincts?
- What would make this research's findings hold up if a skeptical stakeholder challenged the sample size or method?

## Improvement Loop

After each study, note whether the chosen method and sample size were the right call in hindsight — too thin to be convincing, or more than the decision warranted. Feed that judgment into the next research plan, and use concrete examples (a well-scoped study, a guide that surfaced unexpected signal) as evidence of "Voice of the Customer" in a coaching or review conversation.
