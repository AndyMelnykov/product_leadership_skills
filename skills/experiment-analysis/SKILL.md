---
name: experiment-analysis
description: Analyze a concluded A/B test or experiment and produce a read that respects statistical validity -- result summary, significance check, practical significance, and a ship/kill/extend/inconclusive recommendation. Use after an experiment concludes and someone needs to decide what to do with the result, not while it's still running.
argument-hint: "<the experiment result: sample sizes, effect size, significance data, run duration, and what decision it's meant to inform>"
---

<!-- sourcing: drafted-fresh -->

# Experiment Analysis

Turn a concluded experiment's raw result into a read that respects statistical validity, distinguishes statistical from practical significance, and ends in a clear ship/kill/extend/inconclusive call.

## Usage

```
/experiment-analysis $ARGUMENTS
```

## Competency Connection

This skill exercises two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Fluency with Data** (under **Customer Insight**) — defined there as using data to generate actionable insights and digging for the causal relationship between behavior and outcomes, not just reporting a number. Correctly separating "the numbers moved" from "the numbers moved for a reason we can trust" is exactly that competency in practice.
- **Business Outcome Ownership** (under **Product Strategy**) — the model calls this the single most important competency at every level. A ship/kill/extend call that's traceable to the actual statistical and practical evidence, rather than to whoever wants the experiment to have worked, is what ownership of the outcome looks like when the data is ambiguous.

This skill is the analysis half of the experiment lifecycle this repo doesn't yet fully cover — `generate-experiment-plan` (backlog, see `docs/skills-gap-audit.md`) would cover the design half; this skill covers reading the result once it's in.

## Required Inputs

- **Sample sizes** for each variant (control and treatment).
- **Effect size**: the observed difference between variants, in the metric's own units.
- **Confidence/significance data**: a p-value, confidence interval, or equivalent statistical test result.
- **Run duration**: how long the experiment actually ran.
- **What decision this is meant to inform**, if stated — ship/kill/extend calls should be traceable back to a real decision, not produced in a vacuum.

## If Inputs Are Missing

- **No significance data provided**: refuse to declare a winner. Describe the observed difference plainly, but label it explicitly as not yet statistically validated — do not let an eye-catching effect size stand in for a significance test (see Constraints).
- **Sample size or run duration missing**: ask for it before assessing validity. A significance figure without knowing the sample size or duration behind it can't be sanity-checked (e.g., a result that reached significance in an unusually short run may reflect a novelty effect, not a stable one).
- **No stated decision this is meant to inform**: proceed with the analysis, but note in the output that the ship/kill/extend recommendation is generic rather than tailored to a specific business decision, since none was given.

## Process

1. Confirm sample sizes, effect size, significance data, and run duration are all present. If significance data is missing, stop short of a winner call (see Constraints) but still complete the rest of the analysis with what's available.
2. Summarize the observed result: what changed, by how much, for which variant.
3. Run the statistical validity check: does the sample size and run duration support the significance claim being made? Flag known risks even when significance data is present — e.g., a result driven by an unusually short run, or a metric known to be noisy at this sample size.
4. Separate statistical significance from practical significance: even a "real" (statistically significant) effect may be too small to justify the cost of shipping it, and vice versa a large observed effect that isn't yet significant may be worth extending the test to confirm.
5. If segment-level data is available, note whether the effect is consistent across segments or concentrated in one — a result driven entirely by one segment changes the recommendation differently than a uniform effect.
6. Produce a recommendation: ship, kill, extend (run longer or with more traffic), or inconclusive. Every recommendation must be traceable to the validity check and practical-significance judgment above it, not asserted on its own.
7. List caveats: anything that should make a reader trust this result less than the headline number suggests (novelty effects, external events during the run window, multiple comparisons if several metrics were tested).

## Constraints

- **Never declare a winner without significance data.** If it isn't provided, describe the observed difference and label it explicitly as not yet statistically validated rather than implying a result that hasn't been tested for significance is a real effect.
- **Never treat statistical significance alone as sufficient to recommend shipping.** A significant but practically trivial effect needs to be named as such, not silently upgraded into a "ship it" call.
- **Never bury a segment-level split that contradicts the headline result.** If the effect is concentrated in one segment or reversed in another, that goes in the main analysis, not an afterthought.
- **Don't recommend "extend" indefinitely as a way to avoid a call.** If the data already supports a clear ship/kill decision, say so rather than defaulting to "run it longer" out of caution.

## Output Format

```
## Experiment Analysis: [Experiment name]

**Result summary:** [What changed, by how much, for which variant]

**Statistical validity check:**
- Sample size: [per variant] -- [sufficient / insufficient / borderline, and why]
- Run duration: [actual duration] -- [any risk this introduces, e.g. novelty effect]
- Significance: [p-value / CI / test result, or "not provided -- no winner declared"]

**Practical significance:** [Is the effect large enough to matter even if statistically significant? State the reasoning, not just yes/no.]

**Segment splits:** [If available -- consistent across segments, or concentrated/reversed in one. If unavailable, state that.]

**Recommendation:** [Ship / Kill / Extend / Inconclusive] -- [one sentence tracing this back to the validity check and practical-significance judgment above]

**Caveats:** [Anything that should lower confidence in the headline result]
```

## Review Checkpoints

- **Verify the recommendation is actually traceable** to the validity check and practical-significance sections above it, not asserted independently of them.
- **Confirm a missing-significance case is clearly labeled as not statistically validated**, not phrased in a way that reads as a soft "yes" to a skeptical stakeholder skimming the summary.
- **Check that a segment-level contradiction, if one exists, made it into the main analysis** rather than being dropped or minimized.
- **Sanity-check the practical-significance judgment against the actual business context** — a human closer to the cost of shipping should confirm the size of the effect is being weighed against the real cost, not a generic threshold.

## Common Mistakes

- **Reporting an effect size with no significance test as if it were a validated result** — "conversion went up 8%" without saying whether that could be noise.
- **Treating "statistically significant" and "worth shipping" as the same thing** when the effect is real but too small to matter.
- **Hiding a segment where the effect reverses** because the headline number still looks good in aggregate.
- **Recommending "extend" as a default hedge** when the data already clearly supports ship or kill.
- **Ignoring run duration** when assessing whether a significant early result might be a novelty effect that fades.

## Practice Questions

- If significance data weren't included in the input, does this output still avoid declaring a winner — or does a confident-sounding effect size sneak through as an implied one?
- Does the practical-significance judgment actually reference the cost or effort of shipping, or is it a restatement of the statistical result in different words?
- If a segment split contradicts the headline finding, would a reader see that in the main analysis, or only by digging?

## Improvement Loop

After a "ship" recommendation, check whether the effect held up in production at the predicted magnitude — a result that was significant in the test but didn't hold up post-launch is a signal to revisit how validity is being assessed (sample size thresholds, run-duration risk, segment checks), not just a one-off surprise. Track how often "extend" recommendations actually get extended versus quietly resolved by shipping anyway; a pattern of the latter means the extend criteria are being set too conservatively.
