# Opportunity: Shift Handoff Context Loss

*Produced by the `opportunity-framing` skill from `02-research-synthesis.md`.*

## Opportunity Statement

Support teams that run multiple shifts without real-time overlap may be losing customer-facing context at the shift boundary — agents re-ask customers questions that were already answered, and at least one account's frontline agent has already stopped trusting the existing handoff mechanism enough to build a personal workaround. The evidence for this is real but thin: interview-only, four participants, three accounts.

## Who Is Affected + Size

Multi-shift support teams **without a real-time overlap window** between shifts (evidenced by Northwind Analytics, 22 agents/3 shifts, and Vantage Metrics, ~140 agents/follow-the-sun). This explicitly does not extend to teams with overlap — Loopwell (8 agents, 2-hour overlap) reported this as a non-problem, which is itself evidence the segment boundary matters.

Size unknown, no sizing data available. Three accounts were interviewed; there is no data on what share of the broader customer base runs multi-shift, non-overlapping support operations.

## Evidence

- Repeated-question / context-loss symptom directly reported — Source: interview, 1 participant (Northwind Analytics Support Team Lead), carried over from Research Synthesis Finding 1 (Confidence: Low).
- Structurally consistent unreliable-handoff pattern — Source: interview, 1 participant (Vantage Metrics Support Agent), carried over from Finding 3 (Confidence: Low; behavioral evidence — a workaround, not a stated preference).
- 18% cross-shift reassignment rate / ~2x reopen rate — Source: interview, 1 participant (Vantage Metrics Support Ops Manager), self-reported from memory, **not** an exported or independently verified data pull. Carried over from Finding 2 (Confidence: Low). This number should not be treated as validated usage data.
- Counter-evidence that the problem doesn't generalize to overlapping-shift teams — Source: interview, 1 participant (Loopwell Support Team Lead), carried over from Finding 4 (Confidence: Low, but structurally distinct segment).
- Unresolved disagreement on solution direction (AI-generated summary vs. structured manual field) — Source: interview, 2 participants taking opposing positions, carried over from Finding 5 (not a confidence-rated finding; reported as an open disagreement).

## Why Now

Vantage Metrics added a third (APAC) shift approximately six weeks before this research was conducted, and its Ops Manager described the problem as having "gotten worse for us specifically since APAC went live" — a real, dated trigger. However, this is a single-account, self-reported observation, not a company-wide or market-wide trend. It should be read as "why now for this one account's growth pattern," not "why now for the whole customer base" — flagged here as segment-specific urgency, not general urgency.

## What's NOT the Opportunity

- Teams with real-time shift overlap (the Loopwell segment) — evidence suggests this isn't a meaningful problem for them; building for this segment isn't justified by anything gathered here.
- The choice between an AI-generated summary and a structured manual field — that is an unresolved solution-format question (Finding 5), not decided by this framing and not part of the opportunity statement itself.
- Customer-facing visibility into handoff notes or any customer-side tooling — all evidence here is agent- and manager-reported; no customers were interviewed.
- Onboarding, knowledge-base search, or other support-workflow friction not tied specifically to the shift-boundary moment.

## Confidence Level

Low — every supporting finding in the research synthesis was independently rated Low confidence (thin, mostly single-source, with one further-unverified secondhand number). Two participants corroborate the core symptom directionally, but no source is independently verified, and the proposed segment boundary (overlap vs. no overlap) rests on a single data point in each condition.

## Suggested Next Step

Validate further: pull an actual ticket-data export (cross-shift reassignment rate and reopen rate) from Vantage Metrics or a comparable non-overlapping multi-shift account, and interview 2-3 more frontline agents (not just team leads/ops managers) to check whether Jordan's distrust of the existing handoff field is common or idiosyncratic. Confidence should not be treated as Medium or High, and this skill would not on its own recommend proceeding to `write-intent`, until at least the reassignment/reopen numbers are independently confirmed.

That said, this skill produces a framing for a human to act on, not a decision — a human reviewer may reasonably judge that Vantage Metrics' recently-compounding pain (the APAC-shift trigger above) justifies drafting a narrow, explicitly-caveated intent in parallel with further validation, rather than waiting on it. If that judgment is made, the resulting intent doc must carry the Low confidence and unresolved solution-format question forward plainly, not smooth them over.
