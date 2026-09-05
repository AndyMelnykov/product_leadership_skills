# Shift Handoff Context (v1: Structured Field)

*Produced by the `write-feature-spec` skill from `04-intent.md`.*

## Problem

Support teams running multiple shifts without real-time overlap lose context when a ticket crosses a shift boundary, causing agents to re-ask customers things they've already answered. At Vantage Metrics (~140 agents, follow-the-sun), this has visibly compounded since a third shift was added roughly six weeks ago, and at least one frontline agent there has already stopped using the current handoff mechanism in favor of a personal workaround.

## Goals / Non-Goals

- **Goals:** Give agents a short, structured handoff block on tickets that cross a shift boundary — status, what's been tried, what the customer expects, and any blocker — so the incoming agent has usable context without reading the full thread.
- **Non-goals (explicitly out of scope):**
  - AI-generated handoff summaries. Not decided against — this remains an open strategic question carried from the intent doc — but v1 scopes to a structured field specifically so we can test whether the adoption problem is about trust/format before investing in generation.
  - Teams with a real-time shift-overlap window (evidence suggests this isn't a meaningful problem for them).
  - Any customer-facing visibility into handoff content — internal agent tooling only.
  - Weekend/off-hours coverage gaps — a staffing question, not addressed by this feature.

## Assumptions

- Agents will fill in a short structured field if it's meaningfully faster than today's free-text field. **This is a risky assumption**, not a safe one — one Vantage Metrics agent has already abandoned the existing handoff field entirely (see Open Questions/Risks).
- The "non-overlapping multi-shift" segment can be identified from each account's existing shift-configuration data in Relay. Unconfirmed — nobody has verified this data is reliably populated.
- Vantage Metrics' self-reported ~18% reassignment / ~2x reopen figures are directionally useful for justifying that this is worth scoping, but are not used as a target baseline anywhere in this spec (see Success Metrics) because they were recalled from memory, not exported.

## User Flow

1. A ticket is still open when the account's configured shift boundary is reached.
2. The outgoing agent is prompted in-app to fill a short structured handoff block before the ticket reassigns: Status / What's been tried / What the customer is expecting / Blocking item (or "none").
3. **Edge case — field left blank:** the ticket reassigns anyway, but is flagged with a visible "No handoff context provided" badge so the incoming agent knows to check the full thread rather than assume nothing happened.
4. The incoming agent opens the ticket and sees the structured handoff block pinned above the raw ticket history.
5. **Edge case — multiple boundaries in one day** (the compounding scenario Vantage Metrics described after adding a third shift): whether handoff blocks stack (one per boundary) or only the most recent is shown is **not resolved in this spec** — see Open Questions/Risks.
6. **Edge case — race condition:** a shift boundary is reached while the customer is actively replying. Behavior is undefined; needs engineering input before build.

## Success Metrics

- **Primary: Not yet instrumented.** No verified baseline exists for cross-shift reassignment or reopen rate — the only figures we have (Vantage Metrics' self-reported ~18%/~2x) were recalled from memory, not pulled from an export, and should not be used as a baseline. Proposal: instrument reassignment rate and reopen rate on the pilot account(s) for 2–4 weeks before committing to a numeric target.
- **Guardrails:** Average time-to-close on shift-crossing tickets should not increase (the structured field must not add meaningful overhead); support CSAT on pilot accounts should not decline.
- **Target:** Not yet set — depends on the baseline period above. Date TBD once that baseline is established.

## Open Questions / Risks

- Whether the long-term mechanism should be an AI-generated summary or stay a structured field is unresolved (carried from the intent doc); this v1 deliberately scopes to structured only and should be revisited once adoption data exists.
- **Adoption risk:** at least one agent has already opted out of the current handoff mechanism entirely. If that reflects distrust of the mechanism generally (not just its current format), a shorter structured field may not fix the underlying problem.
- Multi-handoff-chain behavior (a ticket crossing more than one shift boundary per day) is unresolved and needs a product decision before build, not during it.
- The race condition between a shift-boundary trigger and an in-flight customer reply is unresolved and needs engineering input.
- The segment boundary itself (overlap vs. no overlap) rests on one account in each condition from the underlying research; if it's wrong, this feature may be scoped to the wrong accounts.
- An independently verified reassignment/reopen-rate pull (not a manager's recollection) is still needed before any numeric success target can be set.

## Rollout Plan

- Feature-flagged, starting with 1–2 design-partner pilot accounts in the non-overlapping multi-shift segment. Vantage Metrics is the strongest-signal candidate, given its recent APAC-driven compounding and its Ops Manager's engagement in the underlying research — pending their willingness to pilot and to share a verified ticket-data export.
- Instrument reassignment and reopen rate throughout the pilot window before any wider release, since no verified baseline currently exists.
- Do not extend to accounts with real-time shift overlap; a request from such an account should be treated as a signal to revisit the segment boundary, not a reason to expand rollout early.
