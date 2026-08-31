# 003: Evaluate skills with YAML eval cases, not narrative QA

## Context

There is no application code to unit-test (see
[001](001-markdown-skills-not-custom-agent-code.md)), but a `SKILL.md` can
still fail in specific, predictable ways: fabricating a metric that was never
provided, silently resolving an ambiguous scope instead of flagging it,
skipping a competency category when there's no evidence rather than noting
the gap. "The demo worked once" does not catch these.

## Options considered

- **No formal evaluation.** Rely on the skill's own "Common Mistakes" prose
  and manual spot-checks. Cheap, but not reproducible and not inspectable by
  someone who didn't write the skill.
- **Narrative QA notes.** A written record of a few manual test runs per
  skill. Better than nothing, but not a fixed, re-runnable check.
- **Structured eval cases.** One YAML file per known failure mode, each
  naming the case and the specific expected behaviors, living in
  `skills/<name>/evals/`.

## Decision

Every skill ships at least one eval case in the `skill / case / expected`
shape, added at the same time the skill is written or retrofitted — not
deferred. Two flagship skills (`synthesize-research`, `write-feature-spec`)
additionally ship a golden `examples/strong-example.md` /
`weak-example.md` pair; other skills get an `examples/` folder only once real
example content exists for them (an aspirational or empty folder is treated
as worse than no folder — see `skills/CONTRIBUTING.md`).

## Consequences

- A reviewer can inspect `skills/<name>/evals/*.yaml` to see exactly which
  failure modes a skill was built to resist, instead of trusting a claim that
  it "works well."
- Eval coverage is a tracked, checkable number (currently 9 of 9 shipped
  skills have at least one eval case) rather than an unverifiable claim.
- This does not catch everything a full test harness would — there is no
  automated runner executing these cases against a live model today; they are
  a reviewable specification of expected behavior, not (yet) a CI gate. That
  gap is listed in the README's "Limitations" section.
