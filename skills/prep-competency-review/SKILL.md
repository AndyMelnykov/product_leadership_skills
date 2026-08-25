---
name: prep-competency-review
description: Prepare a performance review, coaching conversation, or interview rubric using the PM competency model, with evidence organized by competency. Use when a manager needs to write or calibrate a performance review, prepare interview questions, or check whether review and hiring standards for a PM role are actually aligned.
argument-hint: "<review, coaching prep, or interview rubric request, plus who/what it's for>"
---

# Prep Competency Review

Organize evidence, feedback, or interview questions by competency, using the same standard across coaching, review, and hiring.

## Usage

```
/prep-competency-review $ARGUMENTS
```

## Why This Skill Exists

The [PM competency model](../../../docs/pm-competency-model.md) states its central risk plainly: "if hiring interviews evaluate different signals than performance reviews, the organization creates confusion." This skill exists so that a review, a coaching conversation, and an interview loop all draw from the same four categories and twelve sub-competencies, instead of each being reinvented from scratch.

## 1. Establish the Purpose and Person

Ask, if not already given:
- Is this for a performance review, a coaching conversation, an interview rubric, or a calibration check?
- Who is it for — role, level, and how long they've been in the role?
- What evidence exists already (specs, briefs, syntheses, project outcomes, peer feedback)? Point to the other skills in this folder (`write-feature-spec`, `stakeholder-alignment-brief`, `synthesize-research`) if artifacts from those exist — they are natural evidence sources.

## 2. Organize by the Four Categories

Structure everything around the model's four categories, never inventing new ones:

1. **Product Execution** — Feature Specification, Product Delivery, Product Quality
2. **Customer Insight** — Fluency with Data, Voice of the Customer, User Experience Design
3. **Product Strategy** — Business Outcome Ownership, Product Vision & Roadmapping, Strategic Impact
4. **Influencing People** — Stakeholder Management, Team Leadership, Managing Up

For each sub-competency relevant to this review or rubric:
- **Evidence** (for reviews/coaching): a specific, dated example — not a general impression. "Shipped the onboarding spec with a measurable activation target" beats "good at specs."
- **Gap or growth area**: where the evidence is thin or inconsistent.
- **Interview question** (for hiring): a question that would surface the same signal this evidence demonstrates, so the interview bar matches the review bar.

## 3. Check Alignment Across Uses

If evidence or questions already exist from a prior review cycle or job posting for this role, compare them against this pass:
- Are the same sub-competencies being weighted similarly in review and in hiring?
- Is any interview question testing something no current review criteria actually measures (or vice versa)?
- Flag mismatches explicitly rather than silently picking one standard.

## 4. Write Development-Oriented Output

Per the model's guidance, frame gaps as growth, not judgment:
- Pair each gap with a concrete next action ("more explicit trade-off framing in stakeholder briefs" not "needs to communicate better")
- Note what evidence would resolve ambiguity if a competency's evidence is currently too thin to assess confidently

## Constraints

- **Absence of evidence is a gap, not a silent omission.** If a category has no evidence, say so explicitly rather than skipping it or inferring a rating from general reputation.
- **Never write an interview question that tests something no current review criterion measures, or vice versa**, without flagging the mismatch — hiring and review standards must draw from the same bar.
- **Impressions are not evidence.** "Strong communicator" does not belong in an Evidence field; only a specific, dated example does.

## Output Format

```
# Competency Review Prep: [Person / Role] — [Purpose]

## Product Execution
### Feature Specification
- Evidence: ...
- Growth area: ...
- Interview question (if applicable): ...
### Product Delivery
...
### Product Quality
...

## Customer Insight
### Fluency with Data
...
### Voice of the Customer
...
### User Experience Design
...

## Product Strategy
### Business Outcome Ownership
...
### Product Vision & Roadmapping
...
### Strategic Impact
...

## Influencing People
### Stakeholder Management
...
### Team Leadership
...
### Managing Up
...

## Alignment Check
[Any mismatch found between review criteria and interview/hiring criteria for this role]
```

## Common Mistakes

- **Impressions instead of evidence**: "Strong communicator" is not evidence. A specific brief, meeting, or decision is.
- **Skipping categories with no evidence**: Absence of evidence is itself information — note it as a gap rather than omitting the category.
- **Different bar for hiring vs. review**: Writing an interview question that's easier or harder than what current performance review actually holds people to.
- **Judgment framing over growth framing**: The model calls for reducing bias and supporting growth — write gaps as next steps, not verdicts.

## Practice Questions

- For each competency, is there real evidence, or are you inferring from general reputation?
- If this same rubric were applied to a hiring interview tomorrow, would it test the same things this review just evaluated?
- Which sub-competency has the thinnest evidence across the whole team, not just this one person?

## Improvement Loop

After a review or hiring cycle, note which competencies were hardest to find evidence for — that's a signal to build a lighter-weight way to capture evidence continuously (e.g., logging specs, briefs, and syntheses as they happen) rather than reconstructing it all at review time.
