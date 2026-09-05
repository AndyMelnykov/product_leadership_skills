# Research Synthesis: Shift Handoff Context Loss on Relay

*Produced by the `synthesize-research` skill from `01-transcripts.md`.*

## Research Overview

- **Methodology:** 4 semi-structured interviews (~30 minutes each), no survey or usage-analytics pull alongside them.
- **Research question:** When a support ticket crosses a shift boundary on Relay, do agents lose context in a way that costs teams real time or customer goodwill — and if so, for which teams?
- **Timeframe:** Interviews conducted August 25–29, 2026, across 3 Relay accounts (Northwind Analytics, Vantage Metrics, Loopwell).

This is a thin evidence base: four interviews, three accounts, no independently pulled ticket data. Every finding below should be read as suggestive, not conclusive, and confidence levels are capped accordingly.

## Key Findings

**Finding 1: Agents re-ask customers questions that were already answered before a shift handoff.**
- **Evidence:** "We probably re-ask the same question three times before a customer gets an actual answer" — Support Team Lead, 22-agent team, no shift overlap (Northwind Analytics). Corroborated indirectly by Support Agent, ~140-agent team (Vantage Metrics), who described the official handoff field as unreliable enough that they route important context outside it entirely.
- **Frequency:** Directly described by 1 of 4 participants (Northwind); indirectly consistent with a second participant's (Jordan, Vantage Metrics) description of unreliable handoffs, though Jordan did not describe the repeated-question symptom specifically.
- **Impact:** Medium-High where it occurs — described as visibly damaging customer sentiment ("I already told you this"), not just an internal inefficiency.
- **Confidence:** Low. This is a hypothesis based on one direct account and one indirect, structurally-consistent account, with no ticket-level data confirming frequency. Priya's own "maybe a third of tickets" estimate was explicitly offered as a guess, not a measurement, and is not treated as a finding on its own.

**Finding 2: At Vantage Metrics, a manager-reported ~18% cross-shift reassignment rate correlates with a self-reported reopen rate roughly double that of single-agent tickets.**
- **Evidence:** "We reassign about 18% of open tickets across a shift boundary in a given week, and the reopen rate on those is almost double the reopen rate on tickets that stay with one agent" — Support Ops Manager, Vantage Metrics.
- **Frequency:** 1 of 4 participants; not corroborated by any other account.
- **Impact:** Potentially high if accurate, since it implies a measurable quality gap tied directly to the handoff moment.
- **Confidence:** Low, and the source should be flagged explicitly: the manager stated he was recalling the numbers from a dashboard he'd viewed the prior week, not reading from an export in front of him. This is a single, unverified, secondhand figure — it should not be treated as validated usage data.

**Finding 3: At least some frontline agents distrust the official handoff-note field enough to have built a personal workaround instead of using it.**
- **Evidence:** "I don't even open the handoff notes anymore, I just DM the next person if it's actually important... I keep my own spreadsheet" — Support Agent, Vantage Metrics.
- **Frequency:** 1 of 4 participants directly; this is a behavioral observation (a workaround), which is stronger evidence of an unmet need than a stated preference would be, but it's still a single source.
- **Impact:** Medium — suggests that whatever mechanism exists today for capturing handoff context isn't trusted by at least some of the people it's meant for, independent of format.
- **Confidence:** Low (single source), labeled a hypothesis rather than a conclusion. Worth noting because it's a behavior, not an opinion — the participant didn't say the field was bad, they described building and using an alternative to it.

**Finding 4: Teams with real-time shift overlap report this as a non-problem.**
- **Evidence:** "We're small enough that it's not really a problem for us... the two people just talk about it directly before the first person leaves" — Support Team Lead, 8-agent team with a 2-hour daily overlap (Loopwell).
- **Frequency:** 1 of 4 participants, but structurally distinct from the other three (the only account with a real-time overlap window).
- **Impact:** Low/none for this segment specifically — the participant volunteered that the only friction is an occasional weekend coverage gap, not the shift-boundary mechanic itself.
- **Confidence:** Low as a general claim, but directionally useful: it suggests overlap structure, not team size alone, may be the variable that predicts whether this problem exists at all. That itself is unconfirmed with only one data point in this segment.

**Finding 5: Sources disagree on whether an AI-generated handoff summary is the right fix — this is not resolved by the interviews and should not be treated as consensus in either direction.**
- **Evidence:** Vantage Metrics' Ops Manager: "If Relay could generate a short summary of what's happened on a ticket... I don't trust our agents to reliably fill in a manual field." Loopwell's Team Lead, responding to the same idea: "I'd be pretty cautious about that... if Relay is writing a summary and it gets something wrong... that's now potentially something an agent repeats back to the customer as fact. I'd rather have a short structured field." The Vantage Metrics frontline agent was noncommittal ("Maybe? ...depends whether it's actually right").
- **Frequency:** 2 of 4 participants took an explicit position (one for automation, one against), 1 was neutral, 1 wasn't asked.
- **Impact:** This is a disagreement about solution direction, not about whether the underlying problem exists — both positioned participants agreed context loss is real (for the segment where it applies), they disagreed on the fix.
- **Confidence:** N/A — this is reported as an open disagreement, not a finding to resolve. It is not clear whether the disagreement reflects different organizational risk tolerance, different team sizes, or something else; it has not been investigated further.

## User Segments / Personas

- **Distributed, non-overlapping multi-shift teams** (Vantage Metrics: ~140 agents, follow-the-sun, no overlap window) — the segment with the strongest and most recently intensified signal (a third shift added ~6 weeks prior). Size estimate: not available beyond this single account.
- **Multi-shift teams without overlap, mid-size** (Northwind Analytics: 22 agents, 3 shifts) — reports the same core symptom (repeated questions) at a smaller scale. Size estimate: not available beyond this single account.
- **Single-shift teams with real-time overlap** (Loopwell: 8 agents, 2-hour overlap) — reports the problem as effectively absent. Size estimate: not available; unclear what share of the customer base this segment represents.

No quantitative data exists to size any of these segments across the broader customer base — this is 3 accounts, not a representative sample.

## Opportunity Areas

- **Reducing context loss at the shift-handoff moment for teams without real-time overlap** — supported by Findings 1 and 2, though Finding 2's numbers are unverified.
- **Making whatever handoff mechanism exists actually trustworthy to frontline agents**, not just present — supported by Finding 3; a mechanism nobody uses doesn't close the gap regardless of format.
- **An explicit, unresolved question of format (automated summary vs. structured manual field)** rather than a single obvious opportunity — supported by Finding 5. Building the wrong one risks repeating Finding 3's failure mode (a mechanism agents route around).

These are listed in order of how directly the evidence supports them, not a business-impact ranking — no data exists yet to rank by impact with confidence.

## Recommendations

1. **Investigate a handoff-context mechanism for non-overlapping multi-shift teams**, tied to Findings 1 and 3. Do not default to an AI-generated summary or a structured field without further validation — Finding 5 shows real disagreement on which is right.
2. **Do not commission engineering work based on Vantage Metrics' 18%/2x figures as-is.** Tied to Finding 2 — pull an actual ticket-data export (from Vantage Metrics or another distributed account) before using any number as a baseline or a business case.
3. **Do not assume this applies broadly across the customer base.** Tied to Finding 4 — confirm whether overlap structure (not team size) is the real predictor before scoping a fix as "for multi-shift teams" generally.
4. **If a structured or automated field is eventually built, validate it gets used** before declaring success — tied to Finding 3, since the existing mechanism's failure mode was adoption, not the concept.

## Open Questions

- What is the actual cross-shift reassignment and reopen rate, pulled directly from ticket data rather than a manager's recollection?
- Would frontline agents actually use a new handoff mechanism (AI-generated or structured), given Finding 3's evidence that at least one agent has already opted out of the existing one?
- Is shift overlap (not team size) the variable that predicts whether this is a real problem for an account? Only one account in each condition was interviewed.
- No customer-side interviews were conducted — all evidence about customer annoyance is agent-reported, not confirmed with customers directly.
- Suggested follow-up: a scoped ticket-data pull from 2–3 non-overlapping multi-shift accounts, and a short survey of frontline agents (not just team leads/ops managers) on whether they use existing handoff fields.
