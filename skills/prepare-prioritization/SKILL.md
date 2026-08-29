---
name: prepare-prioritization
description: Turn a backlog of candidate items into a structured scoring worksheet -- RICE/ICE-style scores plus qualitative flags -- ready for a human prioritization session, without making the prioritization call itself. Use when a roadmap or backlog prioritization meeting is coming up and the raw candidate list needs to be turned into a scoreable, flagged worksheet beforehand; distinct from `compare-options` (which scores 2+ concrete options against confirmed criteria for a single decision) and `write-decision-brief` (which produces a full brief with a recommendation) -- this skill prepares a whole backlog for a scoring session and stops there.
argument-hint: "<the candidate backlog items, and a scoring framework preference if you have one>"
---

<!-- sourcing: drafted-fresh -->

# Prepare Prioritization

Turn a raw backlog into a scored, flagged worksheet a prioritization meeting can actually work from -- and stop before the ranking is mistaken for the decision.

## Usage

```
/prepare-prioritization $ARGUMENTS
```

## Competency Connection

This skill is the practical exercise of two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Product Strategy > Business Outcome Ownership** — the model calls this the single competency that matters equally at every level, from APM to CPO, because it's about connecting product functionality and goals to strategic objectives rather than treating the backlog as a to-do list. Structuring a backlog so each item's likely business impact is visible and comparable (not just "loudest requester wins") is what makes a prioritization session actually about outcomes.
- **Product Execution > Product Delivery** — the model frames this as working with the immediate team to deliver iteratively while staying honest about measuring against goals set up front. A worksheet that flags which items have real impact/effort estimates behind them and which don't is exactly what keeps a delivery team honest about what it's committing to, instead of it discovering mid-sprint that an "easy win" was actually a guess.

## Required Inputs

- **The candidate list** — the backlog items to be scored, each named specifically enough to estimate against (not "various improvements")
- **A scoring framework preference** (RICE, ICE, or another named scale) — or, if none is stated, this skill asks rather than silently picking one (see below)
- **Per-item impact and effort estimates** (or reach/confidence, depending on the chosen framework), where they exist — these are expected to be incomplete for some items; that gap is handled explicitly in Process and Constraints, not treated as a blocker up front

## If Inputs Are Missing

- **No scoring framework named**: do not default silently to RICE or any other scale. Ask which framework the requester wants (or, if they have no preference, offer RICE and ICE as the two most common defaults and ask them to pick) before scoring anything.
- **An item is missing an impact or effort estimate**: do not invent a number to keep the row complete. Mark that item's score as **insufficient data** and move it to the "Items With Insufficient Data" section instead of the scoring table — see Constraints, this is a hard rule, not a judgment call.
- **The candidate list itself is vague** (a paragraph of themes rather than discrete items): ask for it broken into named, individually scoreable items before proceeding — a theme can't be given a single RICE score without collapsing several different bets into one number.
- **An item is described as a strategic bet, technical debt, or compliance-mandated work**: do not force a comparable score onto it just because the table has a column for one. Route it to the Qualitative Flags section instead (see Process step 5) — pure-score ranking a compliance deadline against a feature request produces a number that looks precise and means nothing.

## Process

1. **Confirm the scoring framework.** If one was stated, use it. If not, ask (per If Inputs Are Missing) before doing anything else — scoring against an unconfirmed framework produces a table the requester didn't actually ask for.
2. **Inventory the candidate list.** List every item by name with a one-line description, so nothing gets scored (or flagged) without first being named explicitly.
3. **Gather estimates per item.** For each item, collect the inputs the chosen framework needs (Reach/Impact/Confidence/Effort for RICE; Impact/Confidence/Ease for ICE). Note the source of each estimate (analytics, engineering, a stakeholder guess) — an estimate with no stated source is itself a signal to look at harder in step 4.
4. **Sort items into three buckets before scoring anything further:**
   - Items with enough estimate data to score.
   - Items missing a required estimate — route these to "insufficient data," not the scoring table.
   - Items that are strategic bets, technical debt, or compliance-mandated work — route these to "qualitative flags," regardless of whether estimate data exists for them.
5. **Score the first bucket only.** Compute the score using the confirmed framework and a stated scale, so every number in the table means the same thing. Attach the estimate sources gathered in step 3 next to each score.
6. **Rank the scored bucket by score** — this produces an ordering, not a decision (see Constraints).
7. **Write up the insufficient-data bucket.** For each item, state which specific estimate is missing (impact, effort, or both) and what would need to be gathered before it could be scored.
8. **Write up the qualitative-flags bucket.** For each item, state which flag applies (strategic bet / technical debt / compliance-mandated) and one line on why it doesn't belong in a pure score comparison with the rest of the backlog.
9. **Close with the human-decision note.** State explicitly, in its own section, that this worksheet is an input to the prioritization session, not the outcome of one — the ranking, the insufficient-data list, and the qualitative flags all still require a human to make the actual call.

## Constraints

- **Never let a missing estimate turn into a guessed number.** If impact or effort data is missing for an item, that item's score must be recorded as "insufficient data," not filled in with a plausible-looking placeholder to keep the table tidy. A complete-looking table built partly on invented numbers is worse than an honestly incomplete one, because it hides exactly which rankings are least trustworthy.
- **This skill never presents the ranking as the decision itself.** Sorting items by score produces an ordering the session can start from, not a prioritization call — the output must say so explicitly (see Output Format), and this skill must never phrase its output as "so we should build X first." That call belongs to the humans in the actual prioritization session, who bring context (dependencies, team capacity, politics, timing) this worksheet cannot see.
- **Strategic bets, technical debt, and compliance-mandated items do not get force-ranked against feature requests on a single score.** They get their own section instead. A compliance deadline that "scores low" on reach/impact is not lower priority than a feature that scores high — it's a different kind of decision, and collapsing both into one ranked list erases that difference.
- **State the estimate source, or flag its absence.** A score attached to an unsourced number ("looks like a lot of users") is not more trustworthy than an explicit insufficient-data flag — do not let an ungrounded guess look identical to a sourced estimate in the table.
- **Do not silently pick the scoring framework.** If none was named, this skill's only allowed move is to ask (see If Inputs Are Missing) — inventing a framework and presenting it as neutral is the same failure mode as inventing a score.

## Output Format

```
# Prioritization Worksheet: [backlog/quarter name]

## Framework
[RICE / ICE / other -- confirmed by requester, or the two options offered
and the one selected]

## Scoring Table
| Item | [framework components, e.g. Reach | Impact | Confidence | Effort] | Score | Estimate Source |
| --- | --- | --- | --- | --- | --- | --- |
(only items with complete estimate data appear here, ranked by score)

## Items With Insufficient Data
- [Item name] -- missing: [impact / effort / both] -- what's needed to score it: [specific data]
(repeat per item; these items are explicitly NOT scored or ranked above)

## Qualitative Flags
- [Item name] -- flag: [strategic bet / technical debt / compliance-mandated] --
  why it isn't pure-score-ranked: [one line]
(repeat per item)

## Human Decision Required
This worksheet ranks the scored items, flags the unscored ones, and separates
out items that don't belong on a pure score comparison. It is not a
prioritization decision. The humans in the prioritization session still
decide what actually gets built first, using this worksheet plus context
(dependencies, capacity, timing, politics) this worksheet does not have.
```

## Review Checkpoints

- A human must confirm the scoring framework and the per-item estimates before this worksheet is treated as ready for the session — especially any estimate whose source is a guess rather than data.
- A human must review the "Items With Insufficient Data" list and decide, before the meeting, whether to gather the missing numbers or accept scoring those items later — this skill does not chase down the missing data itself.
- A human must confirm the "Qualitative Flags" bucket is correct — specifically, that nothing was routed there just to avoid an unflattering score, and nothing that genuinely belongs there was left in the scoring table instead.
- **A human, in the actual prioritization session, makes the final call on what gets built first.** This is the single most important checkpoint for this skill: the scored ranking is a starting point for that conversation, never a stand-in for it. No output from this skill should be read, quoted, or forwarded as "the decision."

## Common Mistakes

- **Filling in a plausible number when an estimate is missing.** The single most common failure this skill exists to prevent — a guessed 3/10 impact score looks identical to a real one once it's in the table, and both get treated with the same confidence downstream.
- **Letting the ranked table read as the recommendation.** Presenting the top-scored item first, in bold, with no accompanying "this isn't the decision" language, all but guarantees someone in the meeting treats the sort order as the answer.
- **Score-ranking a compliance deadline or a strategic bet next to routine feature requests.** These items often score low on reach/impact by construction (a compliance requirement doesn't need "reach" to be mandatory) — putting them in the same ranked list as everything else makes them look deprioritized when they aren't comparable at all.
- **Picking a scoring framework without asking.** Defaulting to RICE because it's the most common framework, without confirming that's actually what this requester or team uses, produces a worksheet the session may reject outright.

## Practice Questions

- Pick the highest-scored item in the table — can you point to the actual impact and effort numbers behind it, and their source, or would you be defending a guess?
- Read only the "Human Decision Required" section — if someone forwarded just that paragraph with no table attached, would they still understand this isn't a decision?
- Scan the qualitative flags — is there an item in there that actually has solid estimate data and just scored inconveniently low, rather than genuinely being a strategic bet, tech debt, or compliance item?

## Improvement Loop

After a prioritization session uses this worksheet, track what happened: did the group override the score-ranked order once real context came in (dependencies, capacity), did an "insufficient data" item turn out to matter more than its lack of a score suggested, and did a qualitative-flagged item get argued about because its flag was wrong. Feed that back into how confidently this skill scores and flags the next backlog — a pattern of overridden rankings or contested flags is exactly the evidence a Business Outcome Ownership or Product Delivery review conversation should be built around, and it's also the clearest signal that this skill's own scoring or flagging judgment needs to get more conservative, not less.
