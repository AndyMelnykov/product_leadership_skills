# 001: Markdown skills, not custom agent orchestration code

## Context

This repository could have shipped a Python/TypeScript agent — a program that
calls an LLM API, wires up tools, and orchestrates a workflow — the way an
agentic product repo does. Instead, every skill is a single `SKILL.md`
(instructions in prose, with a YAML frontmatter trigger) that Claude Code
loads and runs natively.

## Options considered

- **Custom agent runtime.** A Python service with its own tool-calling loop,
  prompt templates, and orchestration logic. Gives full control over
  execution but adds a codebase to maintain, version, and keep in sync with
  the model provider's API.
- **Markdown skills executed by Claude Code.** No custom runtime. The
  "program" is the instructions themselves, reviewed and versioned like any
  other document.

## Decision

Ship every skill as a `SKILL.md` file, using Claude Code's native skill
mechanism, per the contract in `skills/CONTRIBUTING.md`.

## Consequences

- A skill is reviewable by a non-engineer product leader — it's prose, not
  code — which matches the repo's audience.
- There is no application code to unit-test, so **quality is enforced through
  evals** (`skills/*/evals/`, one YAML case per known failure mode) instead of
  a test suite. See [003](003-eval-driven-quality-via-yaml-cases.md).
- Runtime behavior depends on Claude Code's own skill-loading and the
  underlying model; the repo has no way to trace or replay a single
  invocation the way an agent codebase could log a request. This is a
  deliberate trade — see the README's "Observability" section.
- Adding a skill costs no infrastructure, which is why the skill count can
  grow quickly (see `docs/superpowers/plans/2026-08-23-product-leadership-skills-expansion.md`)
  without a corresponding growth in operational surface area.
