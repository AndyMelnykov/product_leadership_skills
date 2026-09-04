---
name: eval-plan
description: Turn an AI feature's expected behavior into a set of measurable eval test cases in the skill/case/expected YAML shape, plus the coverage gaps and cadence needed to actually run them. Use when defining how an AI feature's quality will be measured before or after launch, or when a feature spec describes what an AI feature should do but has no eval cases yet.
argument-hint: "<the AI feature's expected behaviors, plus any known failure modes>"
---

<!-- sourcing: drafted-fresh -->
<!-- Search performed per CONTRIBUTING.md "Sourcing a new skill": WebSearch for Anthropic's
     published eval-design guidance turned up anthropics/claude-cookbooks' "building_evals.ipynb"
     (misc/building_evals.ipynb) plus Arize AI's and Anthropic's own "Demystifying evals for AI
     agents" engineering posts. A direct WebFetch of the notebook confirmed it prescribes a
     four-part test case (input prompt, model output, "golden answer", grader score), ranks
     code-based grading over model-based over human grading, and recommends rubric-style
     instructions for open-ended tasks -- useful conceptual material, but it is a general eval
     *methodology* guide with worked grading-code examples, not a skill artifact with this
     repo's contract (specific required inputs, missing-input behavior, constraints, an
     output structure two runs would match). It also does not address coverage-gap tracking or
     eval cadence (pre-launch vs. ongoing), both of which this skill's brief requires as output
     sections. A second search for "claude skill" eval test case generation surfaced Claude's
     own skill-creator eval feature and third-party "test case generator" skills -- these
     generate with-skill/without-skill test cases to validate a *Claude skill itself* works,
     which is a different subject than planning evals for a *product's AI feature* pre/post
     launch. Nothing found meets this repo's bar, so this skill is drafted fresh, using
     Anthropic's grading-hierarchy framing (code-based > model-based > human) as a conceptual
     reference inside Process step 5, and following the same discipline as this repo's own
     context-audit and ai-feature-risk-review skills (formalizing a practice the plan already
     uses for itself, since every other task in this plan already produces eval cases in this
     exact skill/case/expected shape). -->

# Eval Plan

Turn an AI feature's stated expected behaviors -- and any known failure modes -- into a set of boolean-checkable eval test cases in this repo's `skill/case/expected` YAML shape, plus what isn't covered yet and how often to re-run it.

## Usage

```
/eval-plan $ARGUMENTS
```

## Competency Connection

This skill exercises two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Product Quality** (under **Product Execution**) -- the model notes that quality issues rarely move metrics in an obviously attributable way, which is exactly why they get deprioritized, yet poor quality slowly erodes trust and loyalty until a competitor arrives. An AI feature with no eval cases is a quality gap with no way to detect regression once it ships. Turning stated expected behavior into concrete, boolean-checkable test cases -- before launch and as a standing regression suite -- is the evidence that quality was actually instrumented, not just hoped for.
- **Fluency with Data** (under **Customer Insight**) -- the model defines this as using data to generate actionable insights and connecting quantified goals to meaningful outcomes, going beyond just reporting results. An eval suite is exactly this kind of instrumentation for an AI feature: a boolean-checkable case is a measurement, not an impression. A PM who can only say a feature "seems to work well" hasn't operationalized fluency with data; a PM who can point to which specific expected behaviors are covered, and which aren't, has.

## Required Inputs

- **The feature's expected behaviors**: what the AI feature is supposed to do, stated specifically enough to turn into a pass/fail check -- not a vague quality goal. "Refuses to declare a winner without significance data" is usable; "gives good analysis" is not.
- **Known failure modes, if any**: specific ways the feature is known (or suspected) to go wrong -- a category of bad input it mishandles, an edge case it was seen to fail on, a failure a similar feature has had before.

## If Inputs Are Missing

- **Expected behaviors are stated as vague quality goals** ("the AI should be helpful," "responses should be accurate"): ask for the specific, checkable behavior underneath the goal before proceeding. A vague goal cannot be turned into a boolean-checkable case, and producing a case for it anyway would misrepresent what the eval actually measures (see Constraints).
- **Failure modes are not known yet**: do not block on this. Per the brief, still produce eval cases for whatever expected behaviors are stated, and add an explicit "Failure modes to be identified" line under Coverage Gaps rather than silently omitting the topic or refusing to produce output. Unknown failure modes are an open item to flag, not a missing input that halts the skill.
- **No expected behaviors are given at all** (only a feature description with no stated behavior): ask for at least one specific expected behavior before proceeding -- this skill cannot infer what "correct" means for a feature from its description alone, and guessing would produce cases that test the wrong thing.

## Process

1. Collect the stated expected behaviors and restate each one as a specific, checkable claim about output or behavior -- not a quality adjective. If a stated behavior is too vague to make checkable, flag it and ask for the specific version (see If Inputs Are Missing) rather than inventing specificity that wasn't given.
2. Collect any known failure modes. If none are known, do not block -- proceed to step 3 with only the expected behaviors, and note the gap for step 6.
3. For each checkable expected behavior, draft one or more eval cases in the `skill/case/expected` shape (see Output Format): a short `skill` name, a `case` name describing the scenario, an optional `input_summary` describing the input that scenario represents, and an `expected` list of boolean-checkable behavior strings in `snake_case` -- never vague adjectives like "high quality" or "accurate."
4. For each known failure mode, draft at least one eval case whose scenario reproduces the conditions that trigger it, with `expected` entries that state what the feature should do instead of failing that way (e.g. `does_not_hallucinate_a_missing_field` rather than just naming the failure).
5. Decide how each case should be graded, and note it if it isn't obvious from the `expected` strings alone: prefer a deterministic, code-checkable condition (a specific string, format, or structural check) over one that requires a human or model judgment call; reserve model- or human-graded cases for genuinely open-ended behaviors, per the grading-preference framing in this skill's sourcing note.
6. Identify coverage gaps: list any stated expected behavior that has no case yet, any input variation (edge case, adversarial input, empty input) that plausibly matters but wasn't given, and -- if failure modes were unknown at input time -- an explicit "failure modes to be identified" entry rather than silence on the topic.
7. Recommend a cadence for each case or case group: pre-launch only (a one-time gate before shipping change) versus ongoing regression (re-run on every relevant model, prompt, or feature change). Base the split on whether the behavior is about launch-readiness (e.g. a specific edge case fixed for this release) or about a behavior that could silently regress later (e.g. a core expected behavior any future change could break).
8. Compile the Eval Cases, Coverage Gaps, and Suggested Cadence into the Output Format below.

## Constraints

- **Never write an eval case whose `expected` entries are vague quality adjectives** ("is helpful," "sounds natural," "high quality"). Every entry must be phrased so a specific reader -- human or grader -- could mark it true or false against a specific output, per this repo's existing eval files.
- **Unknown failure modes never block the whole skill.** Produce cases for every expected behavior that is stated, and list unresolved failure modes under Coverage Gaps as an open item, not a reason to withhold output.
- **Do not invent expected behaviors, failure modes, or edge cases that weren't stated or plausibly implied by what was stated.** An eval case that tests a behavior nobody asked for creates false confidence in coverage that doesn't exist; if a plausible additional case seems worth having, put it under Coverage Gaps as a suggestion, not silently add it to Eval Cases as if it were requested.
- **A full set of passing eval cases is not the same as "the feature is safe to ship."** This skill measures the specific behaviors it was given; it cannot certify behaviors nobody thought to state. Say so explicitly rather than letting a clean eval plan imply total coverage.

## Output Format

```
# Eval Plan: [Feature Name] -- [Date]

## Eval Cases
skill: [feature-or-skill-name]
case: [scenario-name]
input_summary: >
  [What input/scenario this case represents, stated concretely enough that
  someone else could reconstruct it.]
expected:
  - [specific_boolean_checkable_behavior_one]
  - [specific_boolean_checkable_behavior_two]

skill: [feature-or-skill-name]
case: [next-scenario-name]
expected:
  - [specific_boolean_checkable_behavior]
...

## Coverage Gaps
- [Stated expected behavior with no case yet, and why]
- [Plausible edge case/input variation not covered]
- Failure modes to be identified -- [state this explicitly if failure modes were unknown at input time; otherwise omit this line]

## Suggested Cadence
- **Pre-launch only:** [case(s) that gate this specific release; why they don't need to recur]
- **Ongoing regression:** [case(s) that should re-run on every relevant change; what change would be expected to break them]
```

The `## Eval Cases` section's YAML blocks must be copy-pasteable directly into an `evals/*.yaml` file in this shape -- one file per case, `skill`/`case`/optional `input_summary`/`expected`. If a case's grading approach (from Process step 5) isn't obvious from its `expected` strings alone -- e.g. it needs a human or model judgment call rather than a deterministic check -- note that in one short prose line immediately below that case's YAML block, never inside the block itself, so the block stays plain, copy-pasteable YAML.

## Review Checkpoints

- **A human who owns the feature's quality bar must approve that the stated expected behaviors are actually the ones that matter** -- this skill turns whatever behaviors it's given into cases; it cannot judge whether those are the right behaviors to prioritize.
- **A human should confirm the grading approach proposed in step 5 is actually feasible** before the case is relied on -- a case whose `expected` entry sounds boolean-checkable but actually requires subjective judgment needs a human or model grader, not a false claim of determinism.
- **A human must decide the real cadence for ongoing-regression cases** (e.g. run on every deploy vs. weekly vs. only after a prompt change) -- this skill only distinguishes pre-launch-only from needs-to-recur; picking the actual recurring schedule is an operational decision outside its scope.
- **A human must confirm coverage gaps are actually acceptable to ship with**, especially an unresolved "failure modes to be identified" line -- this skill flags the gap; it does not decide whether the gap is acceptable risk.

## Common Mistakes

- **Writing `expected` entries as vague quality judgments** ("responses are accurate," "output is well-formatted") instead of a specific, checkable claim a grader could actually evaluate against an output.
- **Blocking the whole eval plan because failure modes aren't known yet**, instead of producing cases for the stated expected behaviors and listing failure modes as an explicit open item.
- **Inventing edge cases or failure modes that weren't stated or implied**, and presenting them as if they were requested, rather than surfacing them as suggestions under Coverage Gaps.
- **Treating a complete-looking Eval Cases section as proof the feature is fully covered**, when it only covers what was stated -- Coverage Gaps exists precisely to prevent that false confidence.
- **Assigning every case to "ongoing regression" by default** without considering whether some cases are genuinely one-time, pre-launch gates that don't need to persist as a maintenance burden.

## Practice Questions

- Could a specific reader mark every `expected` entry true or false against a real output, without needing to ask "what do you mean by that"?
- If failure modes weren't known when this plan was written, does the output say so explicitly under Coverage Gaps, or does it just quietly have fewer cases than expected behaviors?
- Does the Suggested Cadence section actually distinguish which cases need to persist as regression checks versus which were only ever about this one release?

## Improvement Loop

After an eval suite from this plan has run for a while, track which cases actually caught a real regression versus which never fired despite being labeled "ongoing regression" -- a case that never fires might be redundant with another case, or might be guarding against something that no longer changes. Also track which Coverage Gaps entries were later filled in with a real case versus which stayed open indefinitely; a persistently unfilled "failure modes to be identified" gap is a signal to go find out what those failure modes actually are, rather than carrying the same open item forward plan after plan.
