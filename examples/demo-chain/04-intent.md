# Intent: Shift Handoff Context for Non-Overlapping Support Teams

*Produced by the `write-intent` skill from `03-opportunity-framing.md`.*

## Intent Statement

For support teams running multiple shifts with no real-time overlap between them, Relay should reduce the customer-facing damage caused by context loss at the shift boundary — specifically, agents re-asking customers things they've already answered, and frontline agents abandoning the current handoff mechanism in favor of private workarounds. This intent proposes moving in that direction; it does not yet commit to a specific mechanism (see Open Strategic Questions).

## Why This / Why Now

The evidence behind this is real but thin, and should be treated that way: four interviews across three accounts, no independently verified ticket data. The opportunity framing this intent is based on was rated **Low confidence** and its own recommended next step was "validate further," not "proceed" — this intent proceeds anyway, by an explicit human judgment call, not because the evidence has strengthened.

The reason to move now rather than wait for that validation: Vantage Metrics (~140 agents, follow-the-sun) added a third shift about six weeks before this research and reports the problem compounding as a direct result — a dated, specific trigger, even though it's a single account's self-report. Separately, a Vantage Metrics frontline agent described having already stopped using the official handoff field and built a personal spreadsheet instead — a behavioral signal (not just a stated complaint) that the current mechanism has failed for at least one real user. Together these suggest the cost of waiting for a full data pull is not zero, even though the case for acting now is not strong on its own.

This is explicitly not a validated business case. It is a judgment call to begin scoping in parallel with the validation opportunity-framing recommended.

## Success Looks Like

An agent picking up a ticket that crossed a shift boundary can tell, without re-reading the entire ticket thread or messaging a colleague, what has already happened and what the customer is still waiting on — and does not ask the customer something already answered. A support lead at a non-overlapping multi-shift account can point to fewer "I already told you this" moments and less agent time spent reconstructing context from scratch.

One participant (Northwind Analytics' Support Team Lead) described the goal informally as wanting handoffs to "feel less chaotic" — that framing is too vague to act on or later verify, so it's rewritten above into two concrete, observable changes: fewer repeated questions to customers, and less time spent reconstructing ticket history. Both can be checked by someone who wasn't in the room; "less chaotic" cannot.

## Explicit Non-Goals

- Teams with a real-time shift-overlap window (the Loopwell-type segment) — evidence suggests this isn't a meaningful problem for them; not building for this segment.
- Any customer-facing visibility into handoff notes or summaries — this is internal agent tooling only.
- Solving weekend/off-hours coverage gaps for small teams (raised tangentially by Loopwell) — that's a staffing and scheduling question, not a Relay tooling gap.
- A general AI-writing or AI-summarization capability across Relay — this intent is scoped to the shift-handoff moment specifically, not a platform-wide AI initiative.

## Known Constraints

No constraints known yet. Nothing about engineering capacity, timeline, or technical feasibility was discussed in the underlying research — this is a gap the approver should close before treating this as committed, not a solved question.

## Open Strategic Questions

- Should the handoff mechanism be an AI-generated summary or a structured manual field? Sources disagree — Vantage Metrics' Ops Manager wants automation and doesn't trust manual compliance; Loopwell's Team Lead distrusts AI-authored, customer-adjacent content and prefers structured fields; the one frontline agent asked was neutral pending accuracy. Not resolved here — this is `write-feature-spec`'s question to scope, informed by further validation.
- Is "has real-time overlap vs. doesn't" actually the segment boundary that predicts this problem, or is it something else (team size, geographic distribution, ticket volume)? Only one account was interviewed in each condition.
- What is the addressable size of the "non-overlapping multi-shift" segment across the full customer base? Genuinely unknown — could be resolved with account-configuration data (shift setup, coverage hours) that wasn't pulled for this research.
- Was proceeding to this intent, ahead of the validation opportunity-framing recommended, the right call? That remains open until the independently verified reassignment/reopen-rate data comes back — if it contradicts Vantage Metrics' self-reported 18%/2x figures, this intent should be revisited.

## Approval Needed From

VP of Product (direction and resourcing) and Head of Customer Support Operations (confirms the segment framing and workaround behavior described here match what Support is actually seeing, before this is treated as a legitimate input to spec work).
