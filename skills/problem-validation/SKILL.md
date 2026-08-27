---
name: problem-validation
description: >
  Check how strong the evidence behind a stated problem actually is before
  it consumes roadmap time, producing either a validation plan (when
  evidence is thin or absent) or a scored, evidence-cited go/no-go
  recommendation (when real evidence already exists). Use before
  committing an opportunity to a roadmap slot, when a problem statement
  or `opportunity-framing` output needs to be checked for evidence
  strength rather than taken on faith, or when a stakeholder wants a
  "should we build this" answer and no supporting evidence has been
  gathered yet.
argument-hint: "<problem statement, plus whatever evidence exists -- or 'none yet'>"
---

<!-- sourcing: adapted-from-https://github.com/assimovt/productskills/blob/main/skills/problem-validation/SKILL.md (MIT licensed) -->

# Problem Validation

Turn a problem statement into a cheap validation plan when no evidence exists yet, or into a scored, evidence-cited recommendation when it does -- never a verdict manufactured from nothing.

## Usage

```
/problem-validation $ARGUMENTS
```

## Competency Connection

This skill is the practical exercise of two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Customer Insight > Fluency with Data** — the model defines this as using data to generate actionable insight and digging for causal relationships rather than just reporting results. This skill operationalizes that: it ranks evidence types by strength (observed behavior and spending outrank survey responses and opinions), forces every score to cite its source, and refuses to average or eyeball a confidence level -- which is exactly the discipline that separates data fluency from data reporting.
- **Product Strategy > Business Outcome Ownership** — the model calls this the one competency that matters equally at every level, from APM to CPO, because it is about being accountable for whether product work actually drives outcomes rather than just shipping. Refusing to commit roadmap time to a problem until it clears an evidence bar set in advance is that accountability in practice: it stops a team from discovering, after the fact, that a quarter went to a problem nobody could actually show was real.

## Required Inputs

- The problem statement itself, stated as a specific claim (not a feature request or a vague complaint)
- Existing evidence, classified by type: observed behavior, money already spent on workarounds, time invested building custom workarounds, direct interview quotes about past behavior, support tickets / forum complaints, survey responses, or explicitly "none yet"
- If this problem statement came out of `opportunity-framing`, its **Evidence** section and **Confidence Level** -- carry those over rather than re-deriving the evidence classification from scratch
- How many independent people/sources the problem has been observed from (a number, not "several" or "a lot of people")

## If Inputs Are Missing

- **No problem statement, or it's really a feature request in disguise** ("users need a dashboard"): do not proceed to scoring. Ask for the underlying problem, or restate the request as the problem it implies and flag that restatement as an assumption needing confirmation.
- **No evidence at all**: this is the expected, common case, not an error. Do not score anything and do not produce a verdict. Produce a **Validation Plan** instead -- see Process and Constraints below. This is the skill's core behavior, not a fallback.
- **Evidence exists but its type is unclear** (can't tell if a claim is observed behavior or a paraphrase of an opinion): treat it as the weakest tier (survey/opinion-level) until it can be sourced more specifically, and flag it as unsourced in the output. Do not round it up to a stronger tier to make the case look better.
- **Evidence exists but comes from fewer than 3 independent people**: proceed, but the branch logic in Process step 4 treats this the same as thin evidence -- it does not clear the bar for a scored "Go."

## Process

1. **Restate the problem** in one or two sentences, as a claim about who is blocked and what's blocking them -- not a solution, not a business metric.
2. **Set the go/no-go criteria before looking at any evidence.** Use the fixed thresholds in Output Format (Validation Score ≥250 = Go, 100-249 = Investigate More, <100 = Kill; minimum 5 independent sources for a "Go") -- write these into the output first, before the evidence section. This step happens even in the no-evidence branch, so the reader can see what bar future evidence will need to clear.
3. **Classify what evidence exists**, ranked strongest to weakest: observed behavior > money spent on workarounds > time invested in custom workarounds > interview quotes about past behavior (Mom Test style -- what they did, not what they'd hypothetically do) > support tickets/forum complaints > survey responses/opinions. If this came from `opportunity-framing`, carry over its Evidence section and Confidence Level rather than re-deriving.
4. **Branch on evidence strength:**
   - **No evidence, or fewer than 3 independent sources, or only survey/opinion-tier evidence**: do not score. Produce the Validation Questions and Cheapest Way to Answer Each sections as a concrete plan -- specific questions, who to ask, and the cheapest method (interviews, a targeted survey, a support-ticket search, a smoke test) for each. State plainly that this is a plan, not a finding.
   - **Evidence clears the bar** (3+ independent sources, at least one tier stronger than survey/opinion): score Frequency, Intensity, Existing Workarounds, and Willingness to Pay (1-5 each, evidence cited per score), multiply into a Validation Score, and compare against the criteria fixed in step 2.
5. **Write the recommendation only in the scored branch.** In the no-evidence branch, the "Recommendation" section states explicitly that no recommendation is possible yet and points back to the plan.

## Constraints

- **No evidence, no verdict.** If no evidence exists yet, this skill must produce a validation PLAN (what to go find out, and how cheaply) -- never a go/no-go call, a score, or a recommendation manufactured from an empty evidence set. This is the repo's evidence-thin rule applied to this skill.
- **Go/no-go criteria must be defined before any evidence is referenced**, not fitted to the data after the fact. The thresholds in Output Format are fixed by this skill, not tunable per-run to make a favorite problem clear the bar -- if a run is tempted to lower the bar because the evidence almost clears it, that is a signal to flag, not to quietly adjust the threshold.
- **Enthusiasm is not evidence.** "I would definitely use that" or a stakeholder's confident assertion does not raise any dimension's score, and hypothetical willingness to pay ("would probably pay") is capped at 3/5 regardless of how it's phrased.
- **No workaround evidence means the problem isn't painful enough to score a "Go," regardless of the other three dimensions.** If nobody has spent money or built a workaround, cap the Validation Score's read as "Investigate More" at best -- do not let high Frequency or Intensity scores alone produce a "Go."
- **Every score must cite its evidence.** A dimension score with no cited source is not a score -- mark it "insufficient evidence" and route to the no-evidence branch for that dimension rather than guessing a number.

## Output Format

Two shapes, depending on the Process step 4 branch. Both start identically.

**No evidence / thin evidence branch:**

```
# Problem Validation: [short name]

## Problem Restated
[1-2 sentences: who is blocked, by what]

## Go/No-Go Criteria (set before any evidence is referenced)
- Go: Validation Score >=250, evidence across all 4 dimensions, 5+ independent
  sources, at least one workaround (spending or built solution)
- Investigate more: Validation Score 100-249, or fewer than 5 sources, or no
  workaround evidence yet
- Kill: Validation Score <100, or no one has tried to solve this themselves

## Current Evidence Strength
None / Thin -- [state exactly what exists and why it doesn't clear the bar,
citing the evidence hierarchy from Process step 3]

## Validation Questions To Answer
- [specific question]
(repeat)

## Cheapest Way To Answer Each
- [question] -> [cheapest method: N interviews, a support-ticket search, a
  targeted smoke test, etc. -- named specifically, not "do more research"]
(repeat, matched 1:1 to the questions above)

## Recommendation
Not applicable -- no scoring recommendation is possible until the plan above
is executed and evidence exists. Do not treat this plan as a green light to
build.
```

**Evidence exists / scored branch:**

```
# Problem Validation: [short name]

## Problem Restated
[1-2 sentences]

## Go/No-Go Criteria (set before evidence below was reviewed)
[same fixed thresholds as above]

## Current Evidence Strength
- Frequency (1-5): [score] -- [cited evidence]
- Intensity (1-5): [score] -- [cited evidence]
- Existing Workarounds (1-5): [score] -- [cited evidence]
- Willingness to Pay (1-5): [score] -- [cited evidence; hypothetical WTP capped at 3]
Validation Score = Frequency x Intensity x Workarounds x WTP = [number]

## Validation Questions To Answer
[Remaining gaps, if any -- a scored problem can still have open questions]

## Cheapest Way To Answer Each
[for the remaining gaps above]

## Recommendation
Go / Investigate More / Kill -- [tie explicitly back to the criteria stated
above the evidence, not re-justified after seeing the score]
```

## Review Checkpoints

- A human must confirm the evidence classification (Process step 3) is accurate before this is shared beyond the immediate team -- especially whether something scored as "observed behavior" is really that, and not a retelling.
- A human must approve the Recommendation (or, in the no-evidence branch, decide whether the Validation Plan is worth commissioning) before this problem is scoped into a roadmap slot or a `write-intent`. This skill produces a plan or a scored recommendation for a human to act on -- it does not unilaterally decide whether to build something.
- If the Validation Score lands close to a threshold boundary (e.g., 240-260), a human should treat that as "Investigate More" territory in practice, not lean on the literal number to force a "Go."

## Common Mistakes

- **Scoring anyway when evidence is thin.** The single most important failure mode this skill exists to prevent: forcing a Validation Score out of zero or near-zero evidence just to produce a tidy number, instead of admitting the honest answer is "we don't know yet, here's the plan to find out."
- **Setting the bar after seeing the data.** Deciding what counts as "enough" evidence only after the evidence is already in front of you is how confirmation bias produces a "Go" for whatever idea was popular going in.
- **Letting Frequency or Intensity carry a "Go" with no workaround evidence.** A problem people talk about but have never tried to solve themselves is usually not painful enough yet, no matter how high the other scores run.
- **Rounding survey/opinion evidence up to a stronger tier** because it makes the case look more solid. If the source is unclear, it stays at the weakest tier until proven otherwise.

## Practice Questions

- If a skeptical stakeholder asked "how do you know this is painful enough to build," could you point to a workaround someone actually built or paid for -- or would you be pointing at enthusiasm?
- Were the go/no-go criteria written down before the evidence was reviewed, or would a different threshold have been picked if the evidence had come out differently?
- If this run produced a Validation Plan instead of a score, would executing that plan actually change anyone's mind -- or is it busywork dressed up as rigor?

## Improvement Loop

After a scored recommendation or a validation plan is acted on, track what actually happened: did a "Go" problem convert into real usage once shipped, did an "Investigate More" problem clear the bar once more evidence came in, did a "Kill" call get revisited later and turn out to be premature. Feed that back into how strictly this skill weights each evidence tier and where the fixed thresholds sit -- this is what keeps "Fluency with Data" pointed at outcomes instead of becoming a scoring ritual, and what gives "Business Outcome Ownership" a real track record to point to.
