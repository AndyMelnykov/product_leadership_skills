---
name: executive-update
description: Turn project or product status into a concise, executive-facing update covering progress, key metrics, risks, and any ask -- distinct from a full stakeholder alignment brief. Use when preparing a recurring exec or board status update, or responding to an ad hoc "what's the state of X" request from a leader.
argument-hint: "<project/initiative name, plus current status, key metrics, blockers, and any ask of the exec>"
---

<!-- sourcing: drafted-fresh -->

# Executive Update

Turn project or product status into a scannable executive update: what's true now, what moved, what's at risk, and what (if anything) is being asked of the reader.

## Usage

```
/executive-update $ARGUMENTS
```

## Competency Connection

This skill exercises two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Managing Up** (under **Influencing People**) — the model defines this as leveraging senior managers and executives to achieve goals and positively influence strategic direction, with alignment (not just communication) as the core skill. A real exec update is direct evidence of this: it shows whether the writer can distill a project down to what a leader actually needs to act on or stay aligned on, without manufacturing urgency or asks that aren't real.
- **Business Outcome Ownership** (under **Product Strategy**) — the model calls this the one competency that matters equally at every level, from APM to CPO. The "Key metric movement" section forces the writer to connect the work back to a business outcome, not just a shipped feature — an update that only reports activity without a metric is not yet evidence of this competency.

Use this as competency evidence: a manager can check whether an update names a real metric and states the ask honestly (including "no ask"), rather than padding the update to look more consequential than the underlying status warrants.

## Required Inputs

- **Current status**: what's actually true right now for this project/initiative (on track, behind, ahead, or blocked), stated against the plan or milestone it's being measured against — not a general impression of "going well."
- **Key metrics**: the specific metric(s) that matter for this initiative, with actual current values and direction of movement (up/down/flat since the last update) — not just "metrics look good."
- **Blockers**: concrete, named blockers or risks slowing the work down (a dependency, a resourcing gap, a technical risk) — not a vague "some challenges."
- **The ask (if any)**: what is specifically being requested of the executive reader — a decision, a resource, an escalation, or nothing at all this cycle.

## If Inputs Are Missing

- **No explicit ask given**: say "no ask this cycle" in the Ask section rather than manufacturing one. Not every update needs a decision from the reader, and inventing an ask to make the update feel more actionable is worse than an honest "no ask."
- **Current status missing**: ask for it before proceeding. A Headline and Progress vs. plan section cannot be written honestly without knowing what's actually true right now — guessing here risks reporting a status the writer never confirmed.
- **Key metrics missing**: proceed, but state explicitly in Key metric movement that no metric was provided, rather than inventing a plausible-sounding number or trend. A flagged gap is more useful to an executive than a fabricated one.
- **Blockers not stated**: ask whether there are genuinely none, or whether that information just wasn't shared yet. Unlike the ask, silence on blockers is ambiguous — assuming "no blockers" when the information was simply missing is more costly than one clarifying question, since it can leave an executive blindsided later.

## Process

1. Confirm the four required inputs are available, following the missing-input behavior above (ask for status and blockers if genuinely absent; proceed with a flagged gap for metrics).
2. Check whether an explicit ask was given. If none was stated, do not infer or manufacture one.
3. Write the Headline: one sentence capturing overall state (on track / at risk / off track, and the single biggest reason why).
4. Write Progress vs. plan: compare current status to the plan or milestone it's measured against, not just a list of completed activity.
5. Write Key metric movement: state the metric, its current value, and its direction since the last update — or flag that no metric was provided.
6. Write Risks/blockers: name each blocker concretely, and its owner or next step if known.
7. Write the Ask: state exactly what's being requested, or "no ask this cycle" if nothing was given.
8. Add an Appendix pointer: a link or reference to where the fuller detail lives (a stakeholder alignment brief, a project doc, a dashboard) rather than inlining that detail here.
9. Assemble the sections into the Output Format below, in order.

## Constraints

- **Never invent an ask when none was given.** State "no ask this cycle" instead of manufacturing a decision, resource request, or escalation to make the update feel more consequential than it is.
- **Never fabricate a metric value or trend when one wasn't provided.** State that the metric isn't available rather than estimating a plausible-sounding number — a flagged gap is honest; an invented number is not.
- **Don't inline the full detail that belongs in a fuller brief.** This skill produces a scannable update, not a complete case; point to a stakeholder-alignment-brief, project doc, or dashboard via the Appendix pointer instead of padding this update with the backup detail.
- **If the update reveals a real decision is needed, don't try to relitigate it inline.** Name the decision in the Ask, and point to (or flag the need for) a proper alignment brief rather than trying to resolve a multi-stakeholder trade-off inside a status update.

## Output Format

```
# Executive Update: [Project/Initiative] — [Date or period covered]

## Headline
[One sentence: overall state and the single biggest reason why]

## Progress vs. Plan
[What's actually happened, measured against the plan/milestone -- not just a list of activity]

## Key Metric Movement
[Metric name]: [current value] ([direction] from [prior value/period]) -- or "No metric available for this cycle" if not provided

## Risks/Blockers
- [Blocker, named concretely] -- owner/next step: [if known]

## Ask
[What's specifically being requested of the reader] -- or "No ask this cycle."

## Appendix
See [link/reference to fuller detail: alignment brief, project doc, dashboard] for full context.
```

## Review Checkpoints

- **Verify the metric is real and current**, not a stale number carried over from a prior update or an estimate presented as a measured value.
- **Confirm the Ask was actually stated by the requester**, not inferred by the writer from general project urgency — if in doubt, this should read "no ask this cycle."
- **Check that a real cross-functional decision hasn't been quietly folded into this update.** If the Ask names a decision with multiple stakeholders or trade-offs, that belongs in a stakeholder-alignment-brief, with this update pointing to it — not resolved here.
- **Confirm the Appendix pointer actually resolves** (a live link or a named, findable document), not a vague "see the team for details."

## Common Mistakes

- **Manufacturing an ask**: Writing "please review and advise" or similar filler when nothing is actually being requested, just to avoid an update that "does nothing." An honest "no ask this cycle" is more useful, not less.
- **Reporting activity instead of status**: Listing what the team did ("shipped three tickets") instead of stating where things actually stand against the plan ("two weeks behind the original launch date").
- **Metric without direction**: Stating a raw number ("NPS is 42") without saying whether that's up, down, or flat from the last update — a number alone doesn't tell the reader anything actionable.
- **Burying the real risk in vague language**: "Some challenges with the vendor" instead of naming the actual blocker and what it will take to clear it.
- **Inlining the whole brief**: Turning the update into a multi-page document because the writer is worried the reader won't click through to the appendix — this defeats the purpose of a scannable update.

## Practice Questions

- If the reader only had 30 seconds, would the Headline alone tell them the one thing they need to know?
- Is there a real ask here, or did "no ask this cycle" get replaced with something invented to look more actionable?
- Does the Key metric movement section show a real number moving in a real direction, or does it just restate that "things are going well"?

## Improvement Loop

After an update goes out, note whether the executive reader had to come back and ask a clarifying question that the update should have already answered (a missing number, an unclear blocker, an ask that wasn't actually clear) — that's a signal to sharpen that section next cycle, not just this one. Also track how often "no ask this cycle" turned out to be accurate versus how often a real ask emerged shortly after — a pattern of asks appearing right after a "no ask" update usually means status is being reported later than it should be, which is itself evidence to raise in a Managing Up coaching conversation.
