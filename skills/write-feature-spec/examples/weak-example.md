# Weak Example: Bulk CSV Export for Team Admins (same input as the strong example)

## Problem

Admins want bulk export.

## Goals / Non-Goals

- Goals: Add bulk CSV export.
- Non-goals: n/a

## User Flow

1. Admin clicks export, gets a CSV. Deactivated members are excluded by default.

## Success Metrics

- Primary: This will increase export completion rate by 34%.
- Guardrails: None specified.

## Rollout Plan

- Ship to 100% of accounts at once.

## Why this is weak

- **Fabricates a specific number** ("34%") with no instrumentation or data behind it — the flagship failure mode this contract exists to prevent.
- **Silently resolves an ambiguous requirement.** Whether to include deactivated members is a real open question (Product and Support disagree on it) — this spec just picks an answer without flagging the trade-off, hiding a decision that should have been made explicitly.
- **No open questions or risks section at all** — nothing signals what's still undecided, so a reader can't tell what to push back on.
- **"Admins want bulk export" isn't a problem statement.** No who, no why-now, nothing that justifies prioritizing this over anything else.
- **No error or edge-case states.** What happens with a very large team? Unaddressed.
