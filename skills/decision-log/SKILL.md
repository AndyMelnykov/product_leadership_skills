---
name: decision-log
description: Append a durable, append-only entry to a product decision log (what was decided, why, by whom, and what would trigger revisiting it), or query the existing log for prior entries relevant to a new question. Use after any decision brief is approved and needs to be recorded, or when asked "what did we decide about X and why" and the log needs to be checked for a prior answer.
argument-hint: "<the decision, plus rationale, date, and decision-maker -- or the question to look up against the existing log>"
---

<!-- sourcing: drafted-fresh -->

# Decision Log

Record a product decision as a durable, append-only log entry, or query the existing log for what was already decided about a topic.

## Usage

```
/decision-log $ARGUMENTS
```

## Competency Connection

This skill exercises two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Stakeholder Management** (under **Influencing People**) — the model defines this as proactively identifying stakeholders affected by a decision and factoring their requirements into it. A maintained decision log is direct evidence of this: the Decided by and Rationale fields show whether stakeholders were actually named and their input weighed *before* the decision was made, rather than surfacing only after someone complains they were never looped in.
- **Strategic Impact** (under **Product Strategy**) — the model defines this as understanding and contributing to business strategy and bringing it to fruition through consistent delivery of outcomes. A rationale that ties a decision back to strategy or evidence — not to convenience or the loudest voice in the room — is evidence a PM is operating at this level, and a log that accumulates entries over time is evidence of consistency, not just one good call.

This skill also fills a structural gap in this repo: per [CONTRIBUTING.md](../CONTRIBUTING.md)'s Source Hierarchy, "Approved decision" is the highest-authority source any skill's Process can cite when resolving a conflict between inputs — and until this skill, no skill in this repo actually produced that artifact. Every entry this skill appends becomes the canonical record that a working draft, meeting note, or agent inference should defer to when they disagree with it.

## Required Inputs

- **The decision**: the specific choice being logged, stated as a decision, not a topic — "we will limit v1 to English-only" not "localization."
- **The rationale**: why this choice was made — the reasoning, trade-off, or evidence that drove it, not just the fact that it was decided.
- **Date**: when the decision was made (not necessarily the date it's being logged, if the two differ) — an append-only entry loses its value as a timeline without this.
- **Decision-maker**: who actually made or owns the call — a name or role, not "the team," unless the team genuinely decided by consensus and that's stated explicitly.

## If Inputs Are Missing

- **No rationale given**: never log a decision without a stated rationale. Ask for it rather than inferring one from context or from what seems like the obvious reason — an unexplained decision in the log is worse than no entry at all, because it looks authoritative while being unverifiable.
- **No date given**: ask for it before logging. An entry without a date can't be placed on the decision's timeline or checked against when circumstances changed, which defeats the purpose of an append-only historical record.
- **No decision-maker given**: ask for it before logging. An entry without a named owner can't be verified or followed up on, and "who decided this" is often exactly what a future query against this log is trying to answer.
- **Query mode finds nothing relevant**: don't silently return an empty result. State explicitly that no relevant prior entry was found, and say whether that's because the log doesn't cover this topic yet or because it's a genuinely new question.

## Process

First, determine which mode is being requested: appending a new entry, or querying the log for prior entries relevant to a new question. Do not force one mode's steps onto the other.

### Mode 1: Append a new entry

1. Confirm the four required inputs are available: the decision, the rationale, the date, and the decision-maker.
2. If the rationale is missing, stop and ask for it — do not proceed with a plausible-sounding guess (see Constraints).
3. If the date or decision-maker is missing, ask for it before logging (see If Inputs Are Missing).
4. Ask whether there's a known reversibility trigger — a condition that would cause this decision to be revisited. If genuinely none is known yet, record "None specified" rather than inventing one.
5. Check whether this entry corrects, reverses, or supersedes a prior entry already in the log. If it does, do not edit or remove the prior entry — write this as a new entry and reference the earlier one by its date and decision (see Constraints).
6. Assemble the entry in the append-only format below and add it to the end of the log, preserving every existing entry in its original order and wording.

### Mode 2: Query the log

1. Take the question or topic being asked about.
2. Search the existing log entries for any that are relevant to that question or topic.
3. For each relevant entry found, surface it in full — date, decision, rationale, decided by, and reversibility trigger — not just the decision line stripped of its reasoning.
4. If more than one relevant entry exists, present them in chronological order and note explicitly which one supersedes which, if a later entry corrected or reversed an earlier one.
5. If no relevant entry exists, say so explicitly rather than returning nothing or fabricating a plausible-sounding past decision (see Constraints).
6. If a surfaced entry's reversibility trigger appears to have been met by the new question, note that plainly — but do not decide the revisit inline; point to (or propose) a new decision to be logged through Mode 1 once it's actually made.

## Constraints

- **Never log a decision without a stated rationale.** Ask for it rather than inferring one from context — a decision without its "why" is not usable as a canonical record, no matter how confident the inference looks.
- **Never edit or silently overwrite a prior entry.** This is an append-only historical record: a correction, reversal, or update gets a new entry that references the old one by date and decision, so the log always shows what was believed true at each point in time.
- **Never let a query-mode answer fabricate a past decision that isn't actually in the log.** If nothing relevant exists, state that plainly instead of reconstructing a plausible-sounding decision from general knowledge of the project or team.
- **Don't relitigate a decision inside a query response.** If a lookup reveals a decision's reversibility trigger has likely been met, name that fact and point to a proper decision-making process (a new brief, a stakeholder discussion) rather than resolving the change inline.

## Output Format

**Append mode** — one block per new entry, added to the end of the log:

```
## Decision Log Entry — [Date]

**Decision:** [What was decided, stated as a decision, not a topic]
**Rationale:** [Why — the reasoning, trade-off, or evidence behind it]
**Decided by:** [Name or role of the decision-maker]
**Reversibility trigger:** [What would cause this decision to be revisited] -- or "None specified" if genuinely not yet known
```

**Query mode** — one response per lookup:

```
## Decision Log Query: [The question or topic asked]

[One block per relevant entry, in chronological order:]
- [Date] -- [Decision] (decided by [Decided by])
  Rationale: [Rationale]
  Reversibility trigger: [Trigger]

[If a later entry supersedes an earlier one:]
Note: the [later date] entry above supersedes the [earlier date] entry.

[If nothing relevant is found, instead of the blocks above:]
No prior entry in the log addresses [topic/question]. This appears to be a new question, not a change to a previously logged decision.
```

## Review Checkpoints

- **Verify the rationale is actually a reason, not a restatement of the decision.** "We decided to do X because we decided X was right" is not a rationale — a human should reject entries where the rationale field doesn't add new information.
- **Confirm the decision-maker is a real, accountable name or role**, not a placeholder like "leadership" or "the team" used to avoid naming who is actually answerable for the call.
- **Check that the reversibility trigger is concrete and observable**, not vague ("if it doesn't work out") — a human should be able to tell, later, whether the trigger has actually occurred.
- **Confirm a correction was written as a new entry, not an edit to the original.** If a past entry appears to have been altered rather than superseded by a new one, that breaks the append-only guarantee this log exists to provide.

## Common Mistakes

- **Logging the outcome without the reasoning**: "We chose the vendor-hosted option" with no rationale field filled in, or filled in with a repeat of the decision itself.
- **Vague reversibility triggers**: "If it stops working" or "if we change our minds" instead of a concrete, checkable condition like "if monthly active usage of the affected flow drops below X" or "if the vendor's SLA is breached twice in a quarter."
- **Silently editing a past entry** to "clean it up" or correct a mistake, instead of appending a new entry that references it — this destroys the historical record the log exists to preserve.
- **Query mode inventing an answer**: reconstructing what the team "probably" decided from general project context when no actual entry addresses the question, instead of stating plainly that nothing relevant was found.
- **Treating "the team decided" as sufficient** when in fact one person made the call and is describing it as a group decision to diffuse accountability.

## Practice Questions

- If a skeptical stakeholder read only the Rationale field, would they understand why this choice was made — or would they need to ask a follow-up question the entry should have already answered?
- Is the reversibility trigger specific enough that someone could check, six months from now, whether it has actually occurred?
- If queried about a topic the log doesn't cover, would this response honestly say "no prior entry found" — or would it quietly guess at what was probably decided?

## Improvement Loop

After a reversibility trigger is later reported as met, check whether the decision actually got revisited — a trigger that fires with no follow-up action means the log is being written but not consulted, which is worth raising as its own problem. Also track how often query mode turns up "no prior entry found" for questions that, in hindsight, really should have been logged already — a pattern of gaps here means decisions are being made without ever reaching this skill, not that the skill itself is failing.
