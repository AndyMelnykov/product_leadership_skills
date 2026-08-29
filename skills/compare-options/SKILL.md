---
name: compare-options
description: Score 2+ concrete options side-by-side against explicit, confirmed criteria, surfacing where they tie and how fragile the ranking is. Use when 2+ options need to be compared against the same criteria -- as a standalone comparison, or as the reusable building block a broader skill like `write-decision-brief` or a roadmap trade-off analysis calls on for its own options table.
argument-hint: "<the options to compare, and the criteria to score them against, if known>"
---

<!-- sourcing: drafted-fresh -->

# Compare Options

Turn 2+ options into a scored, weighted comparison table, with the ties and the fragile calls called out instead of buried under a single ranked number.

## Usage

```
/compare-options $ARGUMENTS
```

## Competency Connection

This skill is the practical exercise of two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Product Strategy > Strategic Impact** — the model describes this as understanding and contributing to business strategy through consistent delivery of business outcomes. Turning a set of options into an explicit, criteria-based comparison (rather than a gut call) is what lets a leader argue for a choice on strategic grounds, and it's the artifact a broader decision (a vendor pick, a roadmap trade-off) can point back to later as evidence the call was reasoned through.
- **Customer Insight > Fluency with Data** — the model frames this as using data to generate actionable insights and connecting quantified goals to outcomes, going beyond reporting numbers to find what they actually mean. Scoring options against explicit criteria, weighting them, and then checking whether the ranking survives a shift in those weights is exactly this discipline applied to a comparison table instead of a metrics dashboard.

## Required Inputs

- **The options** — at least two concrete, named alternatives to compare (not one option plus vague "other approaches")
- **The criteria** — the specific dimensions the options will be scored against (e.g., cost, implementation time, security posture, vendor stability) — or, if none exist yet, a request to help define them
- Optionally, if known: **weights** for each criterion (how much more one criterion matters than another) — their absence doesn't block the skill, but changes what happens next (see below)

## If Inputs Are Missing

- **Fewer than two options given**: do not proceed. A single option has nothing to be scored against — ask for a genuine second option (or an explicit status-quo/do-nothing baseline) before continuing.
- **No criteria given at all**: do not invent criteria and start scoring. Propose a candidate set of criteria drawn from the options and the stated goal, and stop for explicit confirmation before any scoring happens — see Process step 1. Scoring against self-selected, unconfirmed criteria is the single failure mode this skill exists to prevent.
- **Criteria given but no weights**: proceed, but treat every criterion as equally weighted by default, state that assumption explicitly in the output, and offer to re-run with real weights if the requester has a priority order in mind.
- **Criteria given but vague** ("quality", "fit"): ask for a sharper, more measurable restatement of the vague criterion before scoring against it — a criterion nobody can score consistently produces a table that looks rigorous and isn't.

## Process

1. **Check for criteria.** If none were given, propose a candidate set (drawn from the options themselves and the stated goal) and stop here for explicit confirmation — do not proceed to scoring until the requester confirms or edits the list. This is a hard stop, not a step to note and continue past.
2. **Confirm or assign weights.** If weights were given, use them. If not, state explicitly that criteria are being treated as equally weighted by default, and offer to re-weight if the requester has a real priority order.
3. **Score each option against each criterion**, using a consistent scale (e.g., 1-5) stated once so every cell means the same thing. Attach a one-line justification to any score that isn't self-evident from the option's description — an unjustified number is not evidence, it's a guess with a table around it.
4. **Compute weighted totals** and rank the options from the totals — not from impression.
5. **Identify ties and near-ties.** Where two or more options land within a small margin of each other, say so explicitly and name which specific criterion is actually driving the difference (or confirm there isn't one worth the name "winner").
6. **Run the sensitivity check.** Pick the criterion with the highest weight (or the one the requester seems most confident about) and ask: if this weight shifted up or down by a step, would the ranking change? State plainly whether the top choice is robust or fragile to that shift.
7. **Name what the comparison does not settle.** A scored table answers "which option wins on these criteria as weighted" — not "which option should we pick." State that distinction so the output isn't mistaken for the decision itself.

## Constraints

- **Never silently pick criteria or weights when none were given.** If no criteria exist, this skill's only allowed next step is to propose a candidate set and stop for confirmation — it must never invent criteria, assign its own weights, and produce a scored table as if that were a neutral comparison. This is the repo's evidence-thin rule applied here: an unconfirmed set of criteria is not evidence of what actually matters to the requester.
- **Every score needs a reason a reader can check.** A score that isn't grounded in something stated about the option (a fact, a stated trade-off, an explicit assumption) is not allowed to look identical to one that is — flag ungrounded scores rather than letting the table imply uniform rigor.
- **Ties must be named, not smoothed over.** If a small scoring difference is being reported as a clear winner, that overstates what the numbers actually show — say "effectively tied" when that's what the totals mean.
- **The sensitivity note is mandatory, not optional polish.** A ranking presented with no check on whether it survives a plausible weight change invites false confidence in a number that may be fragile. Skipping this step is skipping the reason this skill exists.
- **This skill produces a comparison, not a decision.** It must not phrase its output as "you should choose X" — that framing belongs to the human (or to a broader skill like `write-decision-brief`) that has more context than a scored table can carry.

## Output Format

```
# Option Comparison: [what's being compared]

## Criteria
[List of criteria, with weight for each -- explicitly marked
"equal weighting assumed" if none were supplied, or "confirmed by requester"
if they were]

## Scoring Table
| Criterion (weight) | Option A | Option B | ... |
| --- | --- | --- | --- |
| [criterion] (w) | [score] -- [justification] | [score] -- [justification] | |
...
| **Weighted Total** | [total] | [total] | |

## Where Options Tie and Why That Matters
[Any options within a small margin of each other, named explicitly, with the
specific criterion (if any) actually separating them -- or a statement that
no meaningful separation exists]

## Sensitivity Note
[Does the ranking change if the highest-weighted (or most-contested) criterion's
weight shifts up or down a step? State plainly: robust, or fragile -- and to
which criterion specifically]

## What This Comparison Does Not Settle
[One line: this scores the stated criteria as weighted -- it is not the
decision itself]
```

## Review Checkpoints

- A human must confirm the criteria (and weights, if supplied) before scoring happens at all — this is the point in Process where the skill is required to stop, not a suggestion.
- A human must sanity-check the score justifications, especially any score that isn't grounded in a stated fact about the option, before this table is treated as a fair comparison rather than a plausible-looking one.
- A human must read the sensitivity note before treating the top-ranked option as settled — a fragile ranking is information the requester needs before acting on it, not a footnote to skip.
- This skill's output is an input to a decision, not the decision. A human (directly, or via a broader skill like `write-decision-brief`) still has to decide what to do with a comparison that shows a tie or a fragile ranking.

## Common Mistakes

- **Scoring before criteria are confirmed.** The core failure this skill is built to prevent: treating a proposed criteria list as final without waiting for confirmation, then presenting the resulting table as if the requester had signed off on what's being measured.
- **Reporting a narrow lead as a clear winner.** Two options three points apart out of a possible fifty is not "Option A wins" — it's a near-tie that deserves to be named as one.
- **Skipping the sensitivity check because the top choice "obviously" wins.** The options where sensitivity matters least are exactly the ones where skipping the check is tempting and cheapest to do — which is also where an unexamined assumption is most likely to hide.
- **Treating equal weighting as a neutral default rather than an assumption.** If no real weights were supplied, equal weighting is a choice this skill made for lack of better information, and the output must say so — not present it as if it were the requester's own priority order.
- **Letting the comparison table imply the decision.** A ranked list with a bolded winner reads as a recommendation even when it isn't one; the "What This Comparison Does Not Settle" line exists specifically to stop that misreading.

## Practice Questions

- Point to the sentence where criteria were confirmed (not just proposed) — is it there, or did scoring start before anyone signed off?
- Pick the least-obvious score in the table — is there a stated justification behind it, or does it just look plausible?
- If the top-ranked option's lead depends on one criterion's weight, does the sensitivity note say so plainly, or would a reader have to reconstruct that themselves from the raw numbers?

## Improvement Loop

After a comparison is used (in a decision brief, a roadmap trade-off, or on its own), track what happened: did the confirmed criteria turn out to be the ones that actually mattered once the choice played out, did a "robust" ranking hold up or did it flip once real weights were reconsidered, and did a flagged tie get treated with appropriate caution or get quietly resolved in favor of a preference. Feed that back into how confidently this skill proposes candidate criteria and how it frames sensitivity next time — this is what keeps a Fluency with Data comparison honest about its own fragility instead of dressing up a close call as a clean win.
