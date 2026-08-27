---
name: define-success-metrics
description: Turn an intent or feature spec into a specific, instrumented set of success metrics -- one primary metric with a target and timeframe, guardrail metrics, leading indicators, and an explicit list of what isn't instrumented yet. Use when writing a spec's Success Metrics section, when a spec or intent already exists but its success criteria are vague, missing, or were left as an open question, when `write-feature-spec` hit unknown analytics context and needs it resolved with a real process instead of a placeholder, or when a team needs to agree on how a launch will be judged before instrumentation work starts.
argument-hint: "<intent or spec to define success metrics for, plus what's currently instrumented vs. not>"
---

<!-- sourcing: drafted-fresh -->

# Define Success Metrics

Turn an intent or spec into the specific, instrumented metrics that will judge whether it worked.

## Usage

```
/define-success-metrics $ARGUMENTS
```

## Competency Connection

This skill is the practical exercise of two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Customer Insight > Fluency with Data** — the model defines this competency as using data to generate actionable insight and connecting quantified goals to meaningful business outcomes, not just reporting a number after the fact. Picking one primary metric with a real target and timeframe, and being explicit about what isn't instrumented yet, is that discipline done on paper before a line of code ships, rather than assumed or backfilled after launch.
- **Product Strategy > Business Outcome Ownership** — the model calls this the single competency that matters equally at every level, from APM to CPO. Naming the exact metric a launch will be judged by, and who signs off that its target is realistic, is what owning the outcome looks like in practice — the alternative is shipping and letting someone else decide after the fact whether it "worked."

## Required Inputs

- **The intent or spec this skill is defining metrics for** — a `write-intent` output, a `write-feature-spec` output, or an equivalent description of what's being built, for whom, and why.
- **What's currently instrumented vs. not** — specifically: which events, properties, or dashboards already track the surface being changed, in which system, and which don't. "We're not sure" is an acceptable answer to capture, but it must be captured, not skipped.
- **The decision or launch date this metric will inform** — so the timeframe in the primary metric is anchored to something real, not invented.
- **Any existing baseline number** — only if one genuinely exists today; this skill never manufactures one (see Constraints).

## If Inputs Are Missing

- **No intent or spec provided**: ask for it. A metric defined against a vague topic instead of a scoped intent/spec can't have a real target — there's nothing to check the target against.
- **Instrumentation state unknown (the core case this skill exists to handle)**: do not assume data will exist. Proceed with the full output structure, but move every metric that depends on unverified instrumentation into "Instrumentation Gaps," and treat that section as a launch blocker — surfaced prominently, not buried at the bottom as a footnote. Never invent a baseline number to make the Primary Metric section look complete in the meantime.
- **No baseline data exists at all, even once instrumentation is confirmed**: say "No baseline known yet" explicitly in the Primary Metric section. Frame the target as directional off a to-be-established baseline (e.g., "establish baseline in the first 2 weeks post-launch, then improve X% off it") rather than fabricating a plausible-sounding starting number.
- **No one is named who can sign off on the target's realism**: proceed, but flag the Review Checkpoint section as an open item to be filled in, rather than silently dropping it or naming a generic "leadership."

## Process

1. **Restate the input.** One or two sentences: what's being built, for whom, and what decision or launch this measurement plan will inform.
2. **Establish instrumentation state explicitly.** For the surface being changed, confirm what's tracked today, where, and at what fidelity. If this is unknown, say so now — it determines how much of the rest of this output lands in "Instrumentation Gaps" instead of the metric sections themselves.
3. **Propose exactly one primary metric.** The single number that tells you this succeeded or failed, with a target and a timeframe. If instrumentation for it doesn't exist yet, still name it here, but list it again under Instrumentation Gaps as a blocker.
4. **Propose guardrail metrics.** What must not get worse as a side effect of optimizing the primary metric. A guardrail only counts if it names a specific way someone could game the primary metric — not a generic "keep an eye on this too."
5. **Propose leading indicators.** Earlier, faster signals that predict whether the primary metric will move, useful for knowing within days or weeks rather than waiting for the full timeframe to elapse.
6. **List metrics considered and not chosen, and why.** This is not filler — it shows the primary metric was chosen deliberately (e.g., rejected because it's a vanity metric, not causally connected to the intent, too lagging to inform the decision, or already covered as a guardrail).
7. **List instrumentation gaps as a launch blocker.** Everything that must be built or turned on before any of the above can actually be measured, stated as action items with an owner if known — not a caveat at the end.
8. **Name the review checkpoint.** Who, by role, must sign off that the primary metric's target is realistic before this measurement plan is treated as final.

## Constraints

- **Exactly one primary metric, never several competing primaries.** A spec with three "primary" metrics has none — it gives the team no way to know if a trade-off between them was a win or a loss. Guardrails and leading indicators exist precisely so other important signals don't need to compete for the primary slot.
- **Never invent a baseline number.** If instrumentation state is unknown or no baseline exists yet, say so explicitly in the Primary Metric section — never fabricate a plausible-sounding starting number or target to make the section look complete. This is the same evidence-thin discipline `write-feature-spec` and `write-intent` already apply, extended to metrics specifically.
- **Instrumentation gaps are a launch blocker, not an afterthought.** They must be surfaced as their own prominent section with action items, never softened into a single caveat sentence buried at the end of the document.
- **A guardrail must name a specific perverse move, not just exist for coverage.** Reject a proposed guardrail that would never actually move in response to gaming the primary metric — it isn't doing guardrail work, it's padding the section.
- **Do not accept vague success language as a metric.** "Engagement will improve" or "this will feel better" is not a metric. Push back and rewrite it into something with a number, a direction, and a timeframe, or explicitly place it in Instrumentation Gaps if no way to measure it exists yet.

## Output Format

```
# Success Metrics: [intent or spec name]

## Primary Metric
[One metric, with target and timeframe. State "No baseline known yet" explicitly
rather than inventing one if none exists.]

## Guardrail Metrics
- [Metric] -- catches: [the specific perverse move this guards against]
(repeat)

## Leading Indicators
- [Metric] -- signals within [timeframe], ahead of the primary metric]
(repeat)

## Metrics NOT Chosen (and why)
- [Metric] -- rejected because [reason: vanity, not causal, too lagging, etc.]
(repeat)

## Instrumentation Gaps
[Launch-blocking list: what must be tracked/built before this plan can be
measured at all, with an owner if known. This section is a blocker, not a
footnote.]

## Review Checkpoint
[Named role(s) who must sign off that the primary metric's target is
realistic before this is final]
```

## Review Checkpoints

- A human must confirm the chosen primary metric actually reflects the outcome the intent/spec cares about — not just the easiest thing already sitting in a dashboard.
- The named role in Review Checkpoint must actually confirm the target is realistic given the current baseline and instrumentation state before this measurement plan is treated as final — this skill proposes a target, it does not approve one.
- Where Instrumentation Gaps lists work, a human (typically engineering or analytics) must confirm the instrumentation plan and timeline before launch — this skill can specify what needs to be tracked, not build or schedule the tracking itself.

## Common Mistakes

- **Naming multiple "primary" metrics.** Pick one; move the rest to guardrails or leading indicators.
- **Treating Instrumentation Gaps as a minor appendix.** If the data won't exist at launch, that is a blocker on knowing whether the launch worked at all — it belongs near the top of what a reviewer reads, not the bottom.
- **Inventing a baseline number to make the Primary Metric section look concrete.** A specific-looking number with no real source is worse than an honest "not known yet" — it gets treated as fact by whoever reads it next.
- **Guardrails that can't actually catch anything.** A guardrail chosen for coverage rather than because it names a real trade-off is decoration, not protection.
- **Letting vague success language survive unedited.** "Improve engagement" reaching the Primary Metric section unchanged means this skill didn't do its job.

## Practice Questions

- If someone challenged the primary metric's target next quarter, would it hold up as a deliberate call — or was a plausible-sounding number invented to fill the section?
- Does each guardrail name a specific way someone could game the primary metric, or could it be deleted without losing any real protection?
- If the instrumentation needed for this plan doesn't exist today, does this output treat that as something that could sink the whole measurement plan — or as a footnote?

## Improvement Loop

After launch, revisit the plan: did the primary metric move as predicted, did any guardrail actually catch a perverse optimization, was the target realistic, and did the instrumentation gaps actually get closed before launch or slip past it unnoticed? Feed specific examples back into how confidently this skill proposes targets and how hard it pushes on instrumentation gaps next time — that is what keeps "Fluency with Data" and "Business Outcome Ownership" evidence honest rather than aspirational.
