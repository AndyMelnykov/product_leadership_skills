---
name: metric-definition
description: Produce a rigorous metric definition doc (exact formula, edge cases, data source, owner) for a named metric, or check whether an existing metric definition is actually computable from the stated data source. Use before building a dashboard, before writing success metrics into a spec, or whenever two people disagree on how a metric is calculated.
argument-hint: "<the metric name and intent, plus what data source it would be calculated from>"
---

<!-- sourcing: drafted-fresh -->

# Metric Definition

Turn a metric name and intent into a rigorous, unambiguous definition — exact formula, edge cases, data source, and owner — that two people can compute independently and get the same number.

## Usage

```
/metric-definition $ARGUMENTS
```

## Competency Connection

This skill exercises **Fluency with Data** (under **Customer Insight**) from the [PM competency model](../../docs/pm-competency-model.md) — defined there as the ability to use data to generate actionable insights and connect quantified goals to meaningful business outcomes. A metric two people compute differently isn't fluency, it's noise wearing a number; writing down the exact formula, edge cases, and data source is the concrete, checkable evidence that a metric is actually usable for a decision rather than just a name on a dashboard.

This skill also fills a gap two other skills in this repo assume is already solved: `build-dashboard` needs a real, agreed definition for whatever it charts, and `define-success-metrics` (Task 15) needs one for whatever target it sets — until this skill, nothing in the repo actually produced that definition as its own artifact.

## Required Inputs

- **The metric name and intent**: what the metric is called, and what question or behavior it's meant to represent — "activation rate" is a name; "the share of new signups who complete the core action within 7 days" is an intent.
- **Data source availability**: what system(s) the underlying data would come from, and whether that source is already accessible (a warehouse table, an analytics tool, a manual export) or still hypothetical.

## If Inputs Are Missing

- **Intent given but no data source stated**: ask which system the data would come from before writing a formula — a formula written against an assumed source is a guess dressed up as a definition.
- **Data source stated but it can't actually support the definition as intended**: say so explicitly rather than defining an uncomputable metric (see Constraints). Name the specific gap (the source has no user-level timestamps, it doesn't distinguish test accounts, etc.) rather than a vague "may not be possible."
- **Existing metric with disputed definitions**: if this skill is invoked because two people already disagree, ask for both existing definitions rather than picking a third from scratch — the disagreement itself is diagnostic input.

## Process

1. Confirm the metric's name and intent are stated as a specific question or behavior, not just a label. If only a label is given, ask what decision or behavior this metric is meant to represent.
2. Confirm the data source and whether it's currently accessible. If unstated, ask before proceeding (see If Inputs Are Missing).
3. Draft the exact formula: numerator, denominator (if a rate), units, and time window.
4. Walk the formula against known edge cases for this kind of metric — test/internal accounts, refunds or reversals, duplicate events, partial time windows, deleted or churned users, timezone boundaries — and state how each is handled. Do not skip this step even if no edge case seems obviously relevant; state "none identified for this metric" only after actually checking the categories above, not by default.
5. Check whether the stated data source can actually produce every field the formula needs. If it can't, stop and flag the specific gap instead of finishing the definition as if it were computable (see Constraints).
6. Assign an owner — the person or role accountable for the definition staying correct as the underlying system changes, not necessarily whoever asked for it.
7. Note the refresh cadence and any known limitations (sampling, lag, a known undercount) that a reader of this metric should keep in mind.

## Constraints

- **Never finalize a definition the stated data source cannot actually support.** If a required field (user-level identity, timestamp granularity, a segment flag) doesn't exist in the source, say so as the primary finding rather than writing a plausible-looking formula anyway.
- **Never leave an edge case unaddressed by omission.** A definition that doesn't say how refunds, test accounts, or duplicate events are handled will be computed inconsistently the first time two people implement it independently.
- **Don't assign "the team" as owner.** An unowned metric definition drifts silently as systems change; name a person or a specific role.
- **Don't infer a business threshold or target as part of this skill.** This skill defines how the metric is calculated, not what value is good — a target belongs to `define-success-metrics`, not here.

## Output Format

```
## Metric: [Name]

**Intent:** [The question or behavior this metric represents]
**Formula:** [Exact numerator / denominator / units / time window]
**Edge cases:**
- [Edge case] -- [How it's handled]
- ...

**Data source:** [System(s) the data comes from]
**Refresh cadence:** [How often the number updates]
**Owner:** [Person or role accountable for the definition]
**Known limitations:** [Sampling, lag, undercount, or other caveats -- or "None known" only if genuinely checked]
```

If the data source cannot support the requested definition, replace the body above with:

```
## Metric: [Name] -- NOT COMPUTABLE AS STATED

**Intent:** [The question or behavior this metric was meant to represent]
**Gap:** [Specifically what the stated data source is missing]
**What would need to change:** [The instrumentation or data-source change required before this can be defined]
```

## Review Checkpoints

- **Verify the formula is actually unambiguous** — a human should be able to hand it to two different analysts and expect the same number back, not a "close enough" range.
- **Confirm every edge case listed is actually handled in the real data source**, not just described in principle — a human familiar with the source should sanity-check this against how the underlying system actually behaves.
- **Check the owner is a real, specific, accountable name or role**, not a placeholder.
- **If marked not computable, confirm the gap is real** (not a workaround the author didn't think of) before treating it as a blocker.

## Common Mistakes

- **Writing a formula without a time window** ("percentage of users who convert" with no window stated), which makes the number silently different depending on who calculates it and when.
- **Skipping edge cases because none seem obvious** rather than actually checking the standard categories (test accounts, refunds, duplicates, timezones, partial periods).
- **Defining a metric the source can't actually compute**, discovered only later when someone tries to build the dashboard — this skill exists specifically to catch that before it happens.
- **Naming "the team" or "analytics" as owner** instead of a specific accountable person or role.
- **Smuggling in a target or threshold** ("good" being >20%) when this skill's job is the definition, not the goal.

## Practice Questions

- If a different analyst implemented this formula from scratch, without asking any follow-up questions, would they compute the same number?
- Does the edge-case list actually reflect how this specific data source behaves, or is it a generic list that wasn't checked against the real system?
- If someone challenged this metric's number next quarter, does the definition give a specific, named owner who could investigate?

## Improvement Loop

After the metric is implemented, check whether the computed number matched what people expected going in — a large surprise usually means an edge case was missed or the intent was misunderstood, not that the metric itself is wrong. Track how often a "not computable as stated" finding turns into an actual instrumentation change versus getting quietly dropped; if it's mostly dropped, the metric probably wasn't as important as the request implied, which is itself useful signal for prioritization work.
