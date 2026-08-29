---
name: write-decision-brief
description: Turn a pending product decision into a written brief -- current state, options, trade-offs, a traceable recommendation, and what's needed to decide. Use when a decision needs to be written down before it's made, for any audience or no audience yet -- distinct from stakeholder-alignment-brief, which is specifically a pre-read for a meeting with stakeholders; use this one when there is no meeting, or the brief needs to stand on its own before an audience is even decided.
argument-hint: "<decision to make, the options on the table, and any known constraints>"
---

<!-- sourcing: drafted-fresh -->

# Write Decision Brief

Turn a decision that's still living in someone's head (or a thread of half-formed options) into a brief that forces a real choice, not a status update.

## Usage

```
/write-decision-brief $ARGUMENTS
```

## Competency Connection

This skill is the practical exercise of two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Product Strategy > Strategic Impact** — the model describes this as the ability to understand and contribute to business strategy, and to bring strategy to fruition through consistent delivery of business outcomes. A decision brief is where that happens concretely: it forces the trade-offs behind a strategic choice into the open, ties a recommendation to a specific business rationale rather than a preference, and creates a record a leader can point to later as evidence a call was reasoned through, not just made.
- **Influencing People > Stakeholder Management** — the model frames this competency as factoring stakeholders' requirements into decisions, not just informing them afterward. Even when this brief has no scheduled meeting behind it (the case that distinguishes it from `stakeholder-alignment-brief`), naming who is affected by each option and what they stand to gain or lose is what keeps the eventual decision from landing as a surprise to the people it touches.

## Required Inputs

- **The decision to make**, ideally already stated as a forced choice ("should we do X or Y") rather than an open topic ("let's talk about X")
- **At least one real alternative** to whatever is being proposed — a second option, or an explicit status-quo/do-nothing baseline (see Constraints — this is the one input this skill will not proceed without)
- **Known constraints** bounding the options: budget, timeline, technical limits, org/legal/compliance limits, or "none known yet"
- Optionally, if known: a decision owner and a deadline — their absence doesn't block drafting, but it does get flagged (see below)

## If Inputs Are Missing

- **Only one option given (no real alternative, no status quo named)**: do not proceed to draft trade-offs or a recommendation for it — a single option dressed up with pros and cons is not a decision, it's a pitch. Ask for a genuine second option, or explicitly propose the status-quo/do-nothing baseline as the second option, before continuing. This is a hard stop, not a flag to note and move past.
- **The decision itself is vague or open-ended** ("we should discuss the pricing model"): restate it as a forced-choice question before proceeding, and confirm that restatement captures the actual decision rather than assuming it.
- **Constraints are unknown**: proceed, but say explicitly that trade-offs are drafted without known budget/timeline/technical limits and may look different once those are supplied — do not silently assume constraints that were never given.
- **No decision owner or deadline named**: proceed, but state plainly in the output that no owner is named — an undeclared owner is itself a risk to the decision actually getting made, not a cosmetic gap.

## Process

1. **Restate the decision as a forced choice.** Turn whatever framing was given into an explicit "should we do A or B" question the brief will answer.
2. **Check for a genuine second option.** If only one option exists, stop here and ask for a real alternative or confirm the status quo as the explicit second option (see Constraints) — do not continue to step 3 until this is resolved.
3. **Establish the current state and why now.** What's true today, what happens if nothing changes, and what specifically makes this decision necessary in this period rather than indefinitely deferrable.
4. **Lay out each option concretely** (2-4 total, including the status quo if that's the baseline): what it is, what it costs, what it risks, and who is most affected.
5. **Reconcile the inputs behind each option using the source hierarchy** if they conflict: approved decision > canonical docs > current customer evidence > meeting notes > working drafts > agent inference. State explicitly which input won and why, rather than silently picking one.
6. **Build the trade-offs comparison.** Use the same criteria across every option (cost, risk, what it protects or gives up) so the options are actually comparable, not apples-to-oranges.
7. **Draft the recommendation, traceable to a specific trade-off already listed.** Name the deciding factor. A recommendation that doesn't point back at something in step 6 is not a reasoned recommendation.
8. **Name the risks of the recommended path**, and how they'd be mitigated or monitored — not just the upside case.
9. **State the decision needed**: the forced-choice question, the owner (or "no owner named" if unknown), the deadline (or "no deadline given"), and what happens by default if no decision is made by then.

## Constraints

- **If only one option was given, do not draft trade-offs for it as if it were a real comparison.** Ask for a genuine alternative, or make the status-quo (do-nothing) baseline the explicit second option, before proceeding. A brief that evaluates a single path against itself is not a decision brief — it's advocacy wearing a decision brief's format, and it will not hold up when someone asks "compared to what?"
- **Never state a recommendation that isn't traceable to a trade-off already listed above it.** If the deciding factor isn't visible in the Trade-offs section, the recommendation is not usable evidence of a real decision process — it's just an opinion with a template around it.
- **State which source wins when inputs conflict, using the repo's source hierarchy** (approved decision > canonical docs > current customer evidence > meeting notes > working drafts > agent inference) — never silently pick one version of the facts over another or average them together.
- **Do not manufacture urgency in "Why Now."** If nothing specific makes this decision time-bound, say so plainly rather than dressing up an evergreen decision as urgent.
- **Do not invent risks or mitigations that aren't grounded in something stated in the brief.** A risks section that reads as generic boilerplate ("execution risk," "market risk") without tying back to this specific decision is worse than a shorter, honest list.

## Output Format

```
# Decision Brief: [Decision]

## Decision
[Forced-choice question] — owner: [name/role, or "no owner named"] — needed by:
[date, or "no deadline given"]

## Why Now
[What specifically makes this decision necessary in this period, or "no
time-bound driver identified -- flagged as not urgent"]

## Current State
[What is true today; what happens if nothing changes]

## Options
### Option A: [name]
- What it is:
- Cost / effort:
- Risk:
- Most affected:

### Option B: [name, or "Status Quo / Do Nothing"]
...
(repeat for any additional real options -- 2-4 total)

## Trade-offs
[Same criteria across every option -- cost, risk, what's protected or given up
-- so the options are genuinely comparable]

## Recommendation
[Recommended option, and the specific trade-off above it points back to]

## Risks
[Risks of the recommended option specifically, and how each would be
mitigated or monitored]

## Decision Needed
[What you need from the owner, by when, and what happens by default if no
decision is made by that date]
```

## Review Checkpoints

- A human decision owner must review and approve the Options and Trade-offs sections before this brief is treated as final — this skill drafts the comparison, it does not decide which option wins. If no owner is named, a human must assign one before the brief is acted on.
- A human must confirm the Recommendation's stated deciding factor actually reflects what matters most to the business, not just the factor that was easiest to write up.
- A human must sign off on the Risks section before the recommended option is greenlit — this skill can surface risks it was told about or can infer from the stated options, but it cannot substitute for a domain expert's judgment on what could go wrong in execution.

## Common Mistakes

- **Treating a pitch as a decision brief.** The single most common failure: one option gets fully fleshed out with trade-offs and risks, while the "alternative" is a token strawman set up to lose. If the second option couldn't plausibly win, it isn't a real alternative.
- **A recommendation that free-floats above the trade-offs.** "We recommend Option A because it's the best choice" without pointing at a specific line in the Trade-offs section is not a reasoned recommendation — it's a conclusion with no visible argument.
- **Skipping the owner and deadline because they feel like formalities.** A decision brief with no named owner and no deadline tends to get read, nodded at, and never actually decided.
- **Padding options to look thorough.** Three options that all amount to the same choice with cosmetic differences doesn't strengthen a decision brief — it dilutes the real comparison the reader is here to make.

## Practice Questions

- If someone asked "compared to what?" about your recommendation, does the brief already answer that, or does it read like the only option that was seriously considered?
- Point at the sentence in the Trade-offs section that your Recommendation is actually built on — is it there, or did you write the recommendation first and the trade-offs to match it after?
- If this decision doesn't get made by the stated deadline, does the brief say what happens by default — or does silence on that point mean nothing will actually happen?

## Improvement Loop

After the decision is made (or the deadline passes with no decision), track what happened: did the chosen option's stated risks materialize, did a risk nobody named turn out to be the real problem, and did naming a default-if-no-decision actually get the decision made on time or not. Feed that back into how this skill drafts the next brief's Trade-offs and Risks sections — a pattern of missed risks or blown deadlines is exactly the evidence a Strategic Impact or Stakeholder Management review conversation should be built around.
