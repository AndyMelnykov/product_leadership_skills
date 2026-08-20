---
name: stakeholder-alignment-brief
description: Draft a stakeholder alignment brief for a decision that needs cross-functional buy-in. Use when a decision has multiple stakeholders with different incentives, a trade-off needs to be made explicit before a meeting, or an update needs to move people from informed to aligned rather than just informed.
argument-hint: "<decision or trade-off that needs stakeholder alignment>"
---

# Stakeholder Alignment Brief

Turn a pending decision into a brief that gets stakeholders to a real answer, not just a status update.

## Usage

```
/stakeholder-alignment-brief $ARGUMENTS
```

## Competency Connection

This skill exercises **Stakeholder Management** under **Influencing People** in the [PM competency model](../../../docs/pm-competency-model.md) (see also [Business_structure_stakeholders/README.md](../../../Business_structure_stakeholders/README.md)). The competency is evaluated on whether ambiguity gets converted into an explicit decision with a named owner — not on how many people were kept informed.

Use this as competency evidence:
- A manager can check whether the brief names a decision owner, a deadline, and explicit trade-offs — the same markers the model's guidance calls out for coaching and review.
- An interview question can ask a candidate to draft a brief for a deliberately ambiguous, multi-stakeholder scenario and be scored against the same checklist below.

## 1. Name the Decision

- What decision needs to be made? State it as a question with a forced choice, not an open topic ("Should we delay launch by two weeks to fix X, or ship on time with a known gap?" not "Let's discuss the launch timeline").
- Who owns this decision? If unclear, say so — an undeclared owner is itself a risk to flag.
- By when does it need to be made, and what happens if it isn't?

## 2. Map the Stakeholders

For each stakeholder or group:
- Their goal or incentive in this decision
- What they stand to gain or lose from each option
- Where their interest is aligned or misaligned with the others

Do not skip the misalignment — naming it is what prevents the meeting from surfacing it as a surprise.

## 3. Lay Out the Options

For each realistic option (2-4, not an exhaustive list):
- What it is, concretely
- Trade-offs: what it costs, what it risks, what it protects
- Who is most affected, positively or negatively

Include a recommendation, but keep it separable from the options so stakeholders can disagree with the recommendation without relitigating the options themselves.

## 4. State the Ask

Be explicit about what you need from each stakeholder: a decision, a resource commitment, an escalation, or just awareness. "FYI" updates and "please decide by Friday" asks should not look the same.

## Output Format

```
# Alignment Brief: [Decision]

## Decision Needed
[Forced-choice question] — owner: [name/role] — needed by: [date]

## Context
[1-3 sentences: why this decision matters now]

## Stakeholders
| Stakeholder | Goal/Incentive | Stake in this decision |
| --- | --- | --- |
| ... | ... | ... |

## Options
### Option A: [name]
- What it is:
- Trade-offs:
- Most affected:

### Option B: [name]
...

## Recommendation
[Your recommendation, and why — kept separate from the options above]

## Ask
[What you need from whom, by when]
```

## Common Mistakes

- **Burying the decision**: If a reader has to infer what's being decided, the brief has failed. Lead with it.
- **False consensus framing**: Presenting only the option you want makes disagreement feel like obstruction instead of legitimate trade-off review.
- **No named owner**: A decision without an owner becomes a status update that nobody acts on.
- **Reason omitted**: Communicating the outcome without the reasoning behind it erodes trust the next time a hard call is made.

## Practice Questions

- Could someone who missed the meeting read this brief and know exactly what was decided and why?
- Which stakeholder's objection did you anticipate — and did the brief address it before they raised it?
- Where did you make a trade-off explicit that could have quietly stayed hidden?

## Improvement Loop

After the decision is made, note which objections came up that the brief didn't anticipate, and whether the stated owner actually made the call. Patterns here — stakeholders consistently surprised, decisions consistently stalling on the same objection — are the concrete examples worth bringing into a coaching or review conversation about Stakeholder Management.
