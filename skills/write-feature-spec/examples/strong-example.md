# Strong Example: Bulk CSV Export for Team Admins

## Problem

Enterprise admins currently export team data one page at a time via the UI, and several support tickets ask for a bulk option.

## Goals / Non-Goals

- Goals: Let team admins export the full team roster and usage data as a single CSV.
- Non-goals (explicitly out of scope): Scheduled/recurring exports (separate ask), export formats other than CSV.

## Assumptions

- Admins want machine-readable output primarily for spreadsheet import, not printing.

## User Flow

1. Admin clicks "Export All" on the team page.
2. System generates the CSV in the background; admin is emailed a download link when it's ready.
3. Error state: if the team has more than 50,000 rows, the export is split into multiple files with a message explaining why, rather than silently truncating.

## Success Metrics

- Primary: **Not yet instrumented.** We do not currently track manual multi-page export attempts, so there's no baseline to set a reduction target against. Proposal: instrument page-by-page export clicks for two weeks pre-launch to establish a baseline before committing to a target.
- Guardrails: Support tickets tagged "data export" should not increase post-launch.

## Open Questions / Risks

- Should the export include deactivated team members? Product and Support disagree; needs a decision before engineering scopes the query.
- Is the 50,000-row split threshold right, or should this be based on file size instead? Needs input from engineering on typical row sizes.

## Rollout Plan

- Feature-flagged to 10% of enterprise accounts first, given the new async email-delivery pattern this introduces.
