---
name: skill-name
description: One or two sentences on what this skill produces, then "Use when ..." with the specific situations that should trigger it -- match the inline-trigger style of skills/synthesize-research/SKILL.md:3, not a bare topic label.
argument-hint: "<what the caller should pass as $ARGUMENTS>"
---

<!-- sourcing: adapted-from-<url> | drafted-fresh -->
<!-- Frontmatter must stay the first thing in the file -- most parsers only
     detect YAML frontmatter starting at byte 0, and the repo's Global
     Constraints require new skills to stay installable via /plugin. Put the
     sourcing comment here, immediately after frontmatter, not above it. -->

# Skill Name

One sentence: what this skill turns into what.

## Usage

```
/skill-name $ARGUMENTS
```

## Competency Connection

Name the category and sub-competency from [docs/pm-competency-model.md](../../docs/pm-competency-model.md) this skill exercises, and one sentence on why its output counts as evidence for that competency (not just that it's "related").

## Required Inputs

List the specific pieces of information this skill needs before it can produce a real output -- name each one, not just the topic area.

## If Inputs Are Missing

State explicitly what happens when a required input is absent: ask for it, proceed and flag the gap as an assumption, or refuse to produce output. Do not leave this implicit -- a reader must be able to point to the sentence that answers it.

## Process

1. First step.
2. Next step.
3. ...

Numbered, in the order the skill actually performs them.

## Constraints

At least one thing this skill must refuse or flag rather than silently do. Every skill needs this section, not just flagship ones -- per the repo's Global Constraints, never let weak or absent evidence convert directly into a confident recommendation, rating, or decision.

## Output Format

The exact section headers or template the output must follow, so two runs of this skill produce comparably-shaped output.

## Review Checkpoints

What a human must check or approve before this output is treated as final or acted on.

## Common Mistakes

The specific failure modes a reviewer should watch for in this skill's output -- not generic writing advice.

## Practice Questions

2-3 questions someone could ask themselves to stress-test whether this skill's output actually holds up.

## Improvement Loop

What to track after this output is used, and how that feedback should change what the skill produces next time.
