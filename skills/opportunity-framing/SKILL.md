---
name: opportunity-framing
description: Turn a synthesized research finding or a raw stakeholder signal into a structured opportunity statement with a clear who/problem/why-now. Use when `synthesize-research` has produced findings that haven't been scoped into an opportunity yet, when a stakeholder hands over a raw signal ("support tickets are up 20% on X") without framing, or before writing an intent/PRD so the problem gets framed and evidence-checked before solutioning begins.
argument-hint: "<research finding, raw signal, or stakeholder claim to frame as an opportunity>"
---

<!-- sourcing: drafted-fresh -->

# Opportunity Framing

Turn a research finding or raw signal into a scoped opportunity statement, honest about how strong the evidence behind it actually is.

## Usage

```
/opportunity-framing $ARGUMENTS
```

## Competency Connection

This skill is the practical exercise of two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Customer Insight > Voice of the Customer** — turning a raw signal or research finding into a claim about who is affected and why, grounded in evidence rather than assumption, is exactly the discipline this sub-competency describes: leveraging feedback in all its forms to understand engagement and drive outcomes, rather than skipping straight from a hunch to a roadmap item.
- **Product Strategy > Strategic Impact** — an opportunity statement is the first artifact that connects a customer signal to a business case; framing "why now" and sizing the audience is what lets a leader argue an opportunity deserves a seat at the strategy conversation, not just a backlog entry, which is the essence of contributing to business strategy rather than only executing it.

## Required Inputs

- The finding or signal itself (a `synthesize-research` output, a support-ticket trend, a sales/CS anecdote, or a stakeholder request)
- Who is asserted to be affected (segment, role, or user type)
- What evidence exists for the claim (interviews, survey data, usage/analytics, support volume — or explicitly "none, this is an opinion/request")

## If Inputs Are Missing

- **No evidence at all (pure opinion, HiPPO request, "I just think...")**: do not produce a confident opportunity statement. Say so explicitly and label the entire output an **Unvalidated Hypothesis** instead — same section structure below, but every claim marked unverified and the Confidence Level capped at "Unvalidated Hypothesis." Do not invent a sizing number to fill the "Who Is Affected + Size" section; state plainly that sizing is unknown until evidence exists.
- **Evidence exists but "who is affected" is vague**: proceed, but flag the vagueness explicitly in the output and ask for a tighter segment before this opportunity moves on to `write-intent`.
- **Evidence exists but its source is unclear** (can't tell where a number actually came from): do not attribute it to a specific source to make it look more solid than it is. Mark it "unsourced" and lower confidence accordingly.

## Process

1. **Restate the raw input.** In one or two sentences, capture the finding or signal as given, without editorializing yet.
2. **Classify the evidence.** Sort what's on hand: interview/qualitative, survey/quantitative, usage/behavioral data, support/sales signal, or none (opinion only). Note source and count for each — if this finding came from `synthesize-research`, carry over its confidence level rather than re-deriving one from scratch.
3. **Identify who is affected.** Name the segment or user type as specifically as the evidence supports — not "all users" unless the evidence actually covers all users.
4. **Estimate size, only from evidence.** If usage/analytics or survey data exists, give a range rather than false-precision point number. If no sizing data exists, say so explicitly rather than guessing.
5. **Articulate why now.** What changed, or what makes this worth acting on in this specific period (a trend, a launch, a competitive shift, a strategic bet) — not "it would be nice eventually."
6. **Draw the non-scope boundary.** State explicitly what this opportunity does NOT cover, so it doesn't silently expand during later solutioning.
7. **Set the confidence level** using the evidence classified in step 2: High only for multiple corroborating sources, Medium for one strong source, Low for thin or single-source evidence, Unvalidated Hypothesis when there is no evidence at all.
8. **Recommend a next step.** Either "validate further" (name the specific evidence that would raise confidence) or "proceed to `write-intent`" (only when confidence is Medium or High).

## Constraints

- **No evidence, no confident opportunity statement.** If the input is opinion/HiPPO with no interview, survey, or usage-data support, the output must be explicitly labeled "Unvalidated Hypothesis," never phrased as a validated opportunity. This is the repo's evidence-thin rule applied to this skill: never let weak or absent evidence convert directly into a confident recommendation.
- **Never invent a sizing number.** If no data supports a "Who Is Affected + Size" estimate, state that sizing is unknown. A plausible-sounding number without a real source is worse than no number — it launders a guess into something that looks like evidence.
- **Do not let "why now" become "why not never."** A weak or manufactured urgency claim ("competitors might do this eventually") must be flagged as weak urgency, not dressed up as a strategic imperative.
- **The non-scope section is not optional.** Every opportunity statement must state what it does NOT cover, even briefly — omitting it is how scope creep starts two steps downstream, once solutioning begins.

## Output Format

```
# Opportunity: [short name]

## Opportunity Statement
[1-3 sentences: who, problem, why it matters]

## Who Is Affected + Size
[Segment/role, and a size estimate ONLY if evidence supports one -- otherwise
"size unknown, no sizing data available"]

## Evidence
- [Evidence item] -- Source: [interview count / survey / usage data / support
  volume / NONE]
(repeat per evidence item; if none exists, state "No evidence -- opinion or
request only")

## Why Now
[What makes this worth acting on in this period, or "no urgency evidence --
flagged as weak"]

## What's NOT the Opportunity
[Explicit non-scope -- adjacent problems or user groups this statement does
not cover]

## Confidence Level
High / Medium / Low / Unvalidated Hypothesis -- [one-sentence justification
tied directly to the evidence classified above]

## Suggested Next Step
Validate further: [specific evidence that would raise confidence]
-- or --
Proceed to `write-intent`: [only if confidence is Medium or High]
```

## Review Checkpoints

- A human must confirm the evidence classification (Process step 2) is accurate before this is shared beyond the immediate team — especially whether something labeled "survey data" is really that, and not a stakeholder's paraphrase of a survey.
- A human must approve the Confidence Level and the resulting next-step recommendation before this opportunity is scoped into a `write-intent` or roadmap conversation. This skill produces a framing for a human to validate and act on — it does not decide whether the opportunity is worth pursuing.
- If the output is an Unvalidated Hypothesis, a human should decide whether it's worth commissioning research at all, rather than treating the hypothesis itself as a green light to build.

## Common Mistakes

- **Upgrading an opinion into an opportunity statement.** The single most common failure: a stakeholder's confident assertion gets written up with the same structure and tone as an evidence-backed finding, erasing the distinction between the two.
- **Sizing from vibes.** "This probably affects most of our enterprise customers" with no number or source behind it. If there's no data, say so plainly.
- **Skipping the non-scope section, or writing it as an afterthought.** A missing or vague non-scope boundary is how a two-week opportunity quietly becomes a two-quarter platform initiative.
- **Confusing "why now" with "why ever."** Almost every opportunity can be justified in the abstract; this section needs a reason this period specifically matters, not a generic case for the idea.

## Practice Questions

- If a skeptical stakeholder asked "how do you know this affects that many people," could you point to the actual source, or would you be paraphrasing a guess?
- Does the Confidence Level match the evidence classified in step 2, or did enthusiasm for the idea inflate it?
- Read the "What's NOT the Opportunity" section alone — would a reader who skipped straight to solutioning still know what not to build?

## Improvement Loop

After an opportunity moves forward (or gets shelved), track what actually happened: did the size estimate hold up once real usage data came in, did the "why now" urgency prove real, did the non-scope boundary get respected once solutioning started. Feed that back into how confidently this skill sizes and scopes the next opportunity — this is what keeps "Voice of the Customer" evidence-grounded instead of optimistic, and what gives "Strategic Impact" claims something real to point to later.
