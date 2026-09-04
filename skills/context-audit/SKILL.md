---
name: context-audit
description: Audit a bounded set of docs or sources (a knowledge base export, a folder of specs, a wiki dump) for stale context, duplicate or conflicting definitions, missing canonical-source designations, and contradictory decisions, surfacing findings for human approval rather than resolving them automatically. Use periodically to check whether a knowledge base has drifted, before onboarding an agent workflow onto a knowledge base, or whenever two documents seem to disagree and no one has flagged it yet.
argument-hint: "<the specific set of docs/sources to audit, plus the topic or scope they cover>"
---

<!-- sourcing: drafted-fresh -->
<!-- Search performed per CONTRIBUTING.md "Sourcing a new skill": WebSearch for
     Anthropic-published examples and community "awesome-claude-skills" lists turned up
     several documentation-audit-style skills (e.g. rampstackco/claude-skills'
     documentation-strategy, Docsbook-io/docs-skills, a "Documentation Audit & Accuracy"
     skill on mcpmarket, dosu.dev's /doc-it). All of them audit code-vs-docs sync, broken
     links, docstring coverage, or general doc-freshness/tiering for a docs *strategy* --
     none of them are built around this repo's specific bar: explicitly citing both sides
     of a contradiction instead of picking one, and treating an undesignated canonical
     source as the finding itself rather than something to infer. None were close enough
     to adapt without rewriting the core mechanic, so this skill is drafted fresh. -->

# Context Audit

Audit a bounded set of docs or sources for stale context, duplicate or conflicting definitions, missing canonical-source designations, and contradictory decisions -- and turn what's found into findings for human review, never into an automatic resolution.

## Usage

```
/context-audit $ARGUMENTS
```

## Competency Connection

This skill exercises two competencies from the [PM competency model](../../docs/pm-competency-model.md):

- **Fluency with Data** (under **Customer Insight**) -- the model defines this as connecting quantified goals to meaningful outcomes and digging for the real relationships in the data rather than just reporting numbers. A knowledge base with two conflicting definitions of the same metric or decision produces confident-looking numbers that are actually noise; surfacing that conflict explicitly, instead of silently trusting whichever doc was read first, is the concrete evidence that "fluency" means checking the data's integrity, not just consuming it.
- **Product Quality** (under **Product Execution**) -- the model notes that quality issues rarely move metrics in an obviously attributable way, which is exactly why they get deprioritized, yet they slowly erode trust until a competitor arrives. Stale or contradictory context is a quality issue in the knowledge base itself: it erodes trust in every downstream decision that cites it. Running this audit and producing a dated, specific findings list is the evidence that quality maintenance is happening, not just assumed.

## Required Inputs

- **The bounded set of docs/sources to audit**: specific files, links, or an export -- named individually or as a clearly scoped folder/collection (e.g. "the 12 docs in the Onboarding wiki space," not "the wiki"). This skill does not crawl a live system, a full wiki, or a repo on its own initiative; it audits exactly what it's handed.
- **The topic or scope the audit is checking**: what these sources are supposed to collectively describe (a metric, a workflow, a product area, a decision history) -- so contradictions and gaps can be judged against a shared subject rather than compared arbitrarily across unrelated docs.

## If Inputs Are Missing

- **No bounded set given ("audit our knowledge base")**: ask for the specific list of docs, files, or an export before proceeding. Do not attempt to enumerate or fetch a live source on the audit's own initiative -- an unbounded audit produces an unbounded, unreviewable findings list.
- **Scope/topic not stated**: ask what these sources are meant to collectively cover. Proceeding without it risks flagging unrelated docs as "contradictory" simply because they address different things.
- **No canonical source designated for a topic covered by the input set**: this is not a missing input to ask about -- it is itself a finding. Report it under "Missing canonical sources" rather than picking the most recent, most detailed, or most authoritative-looking doc and treating that as canonical (see Constraints).

## Process

1. Confirm the bounded set of sources and the topic/scope (see Required Inputs). If either is unstated or open-ended, stop and ask rather than guessing at scope.
2. Inventory each source: its stated topic, its last-updated date or version marker (if present), and its stated or implied owner. Note explicitly when a source has no date or no owner -- that absence is itself relevant later.
3. Group sources that address the same sub-topic, metric, decision, or process so they can be compared directly against each other.
4. Within each group, compare the actual content -- not just titles. Check for: the same metric defined with different formulas, the same decision described with different outcomes or dates, the same process described with contradictory steps.
5. For every group where content disagrees, record it as a contradictory decision or conflicting definition. Quote or closely paraphrase both (or all) sides with their source names -- never resolve the disagreement by silently preferring one, including the more recently updated one (see Constraints).
6. For every topic in scope -- whether covered by one source or several -- check whether a canonical source is explicitly designated: an explicit "source of truth" marker, an owner's statement, or a decision-log entry naming one document as authoritative. If no such designation exists, record it under "Missing canonical sources," even if only one document currently addresses the topic and there's no visible conflict.
7. Check each source's age and owner-confirmation status against a staleness threshold. Default to flagging anything with no update or owner confirmation in the last two quarters (~6 months) unless the user states a different threshold for this domain; ask if the right threshold is unclear rather than assuming.
8. Draft proposed source-of-truth designations for the topics found missing one in step 6. Base the proposal's rationale on the source hierarchy in [CONTRIBUTING.md](../CONTRIBUTING.md) (Approved decision > Canonical docs > Current customer evidence > Meeting notes > Working drafts > Agent inference) -- use it to explain why a candidate is proposed, not to auto-select and present as settled.
9. Compile all findings into the five-section Output Format below, and mark the proposed designations as pending human approval, not as decisions already made.

## Constraints

- **Never silently prefer one source over another when two disagree**, including preferring the more recently updated one. Cite both sources explicitly in "Contradictory decisions (cite both)" and let a human decide -- recency is a data point for that human, not a resolution rule this skill applies on its own.
- **An undesignated canonical source is the finding, not a gap to fill.** If no doc is explicitly marked authoritative for a topic, report that absence under "Missing canonical sources" rather than inferring one from thoroughness, recency, or seniority of the author.
- **Recommended source-of-truth designations are proposals for human approval, never auto-applied.** Nothing in this audit's output should read as if a designation has already taken effect.
- **Stay inside the bounded set the user handed in.** Do not fetch, crawl, or infer the existence of additional sources not included in the input, even if a doc references one.
- **Do not report "no contradiction found" as "verified consistent."** State plainly what was actually compared (same topic, overlapping topic, or single-source topic with no comparison possible) so a reader can tell what silence in a section actually means.

## Output Format

```
# Context Audit: [Topic/Scope] -- [Date]

**Sources audited:** [List of docs/sources, with last-updated date and owner if known]

## Stale Context Found
- [Source] -- last updated/confirmed [date or "unknown"], exceeds the [X]-month threshold. [What's at risk of being wrong.]
- ...

## Duplicate/Conflicting Definitions
- **[Term/metric]**: [Source A] defines it as [...]; [Source B] defines it as [...]. Not reconciled -- both cited, no preference applied.
- ...

## Missing Canonical Sources
- **[Topic]**: no source is explicitly designated as authoritative. [List the source(s) that address this topic, if any, without marking one as canonical.]
- ...

## Contradictory Decisions (Cite Both)
- **[Decision/topic]**: [Source A, with date] states [...]. [Source B, with date] states [...]. These conflict; neither is presented as more correct here.
- ...

## Recommended Source-of-Truth Designations (For Human Approval)
- **[Topic]**: proposing [Candidate source] as canonical, because [source-hierarchy rationale]. Pending approval -- not yet in effect.
- ...
```

If a section has nothing to report, keep the header and state explicitly what was checked (e.g. "No conflicting definitions found among the 4 sources covering this metric" rather than omitting the section).

## Review Checkpoints

- **A human must approve every proposed source-of-truth designation before it takes effect** -- this skill's proposals are a starting point for a decision, not the decision itself.
- **A human familiar with the domain should sanity-check the staleness threshold used** -- six months may be far too generous for a fast-moving pricing doc and far too strict for a stable architecture decision.
- **A human should decide which contradiction gets resolved first** -- this audit surfaces and prioritizes by asking, but does not rank business impact on its own.
- **Confirm the "bounded set" audited was actually complete for the stated scope** -- a human who knows the domain should check whether an obviously relevant doc was left out of the input set, since this skill cannot know what it wasn't given.

## Common Mistakes

- **Quietly resolving a conflict by leading with the newer-looking source** -- even listing one first and treating the other as a footnote is an implicit preference; give both equal weight in the write-up.
- **Treating a single-source topic as automatically fine** -- a topic with only one document covering it can still lack any explicit canonical designation; that's a "Missing canonical sources" finding too, not just a multi-source problem.
- **Conflating "no contradiction found" with "verified consistent"** -- if two sources address only partially overlapping ground, say so, rather than implying full agreement was checked.
- **Auditing beyond the handed-in set** -- following a link or reference inside a doc to pull in an "obviously relevant" source that wasn't part of the original scope.
- **Applying the source hierarchy as an automatic tie-breaker** instead of as the stated rationale behind a proposal that still needs human approval.

## Practice Questions

- For every contradiction listed, could a reader identify exactly which two sources disagree and how, without re-reading the rest of the audit?
- Did I give a silent edge to any source -- through ordering, word choice, or omission -- anywhere the docs actually disagreed?
- Is there a topic covered by only one document where I still checked (and reported) whether it has an explicit canonical designation, rather than assuming single-source means settled?

## Improvement Loop

After an audit's findings are reviewed, track which proposed designations were approved as-is, which were overridden, and which contradictions took longest to resolve -- a pattern of overridden designations usually means the source-hierarchy rationale needs a domain-specific adjustment, not that the audit was wrong to propose one. Also track how often a "stale" flag turned out to still be accurate content despite its age (threshold too aggressive) versus genuinely wrong (threshold about right or too lenient), and adjust the default staleness window for that domain accordingly next time.
