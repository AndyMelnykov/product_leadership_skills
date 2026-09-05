# Demo Chain: Transcripts to Alignment Brief

A worked, end-to-end example showing five skills in this plugin chained together on one fictional scenario — each stage's output is a durable artifact the next stage consumes, not a hand-waved summary. Every numbered file was produced by genuinely running the named skill's own Process and Output Format against the previous file's actual content, honoring that skill's constraints (never inventing a metric, never silently resolving ambiguity, labeling thin evidence as thin) given what the prior stage actually produced.

The scenario: Relay (a fictional support-ticketing product) may be losing customer-facing context when a support ticket crosses a shift boundary. The evidence for this stays thin and only partly corroborated all the way through the chain — that's intentional. A chain where a skill honestly flags weak evidence as weak is a better demonstration of what these skills are for than one that fakes strength at every stage.

## The chain

| File | Produced by | What it does |
| --- | --- | --- |
| [`01-transcripts.md`](01-transcripts.md) | (fictional raw input) | 4 customer interview transcripts across 3 accounts, on one coherent problem: context loss during agent shift handoffs. |
| [`02-research-synthesis.md`](02-research-synthesis.md) | [`synthesize-research`](../../skills/synthesize-research/SKILL.md) | Extracts 5 findings from the transcripts, each rated for confidence, explicitly reporting — not resolving — where two participants disagree on the right fix. |
| [`03-opportunity-framing.md`](03-opportunity-framing.md) | [`opportunity-framing`](../../skills/opportunity-framing/SKILL.md) | Frames the opportunity, states plainly that sizing is unknown, and rates overall confidence Low because every underlying finding was rated Low — it does not average or round up to make the opportunity look stronger. |
| [`04-intent.md`](04-intent.md) | [`write-intent`](../../skills/write-intent/SKILL.md) | Turns the opportunity into an approvable intent, rewrites a stakeholder's vague "make it feel less chaotic" into an observable success statement, and carries the Low-confidence caveat forward instead of smoothing it over. |
| [`05-feature-spec.md`](05-feature-spec.md) | [`write-feature-spec`](../../skills/write-feature-spec/SKILL.md) | Turns the intent into a spec with a named Problem, Goals/Non-Goals, User Flow (including edge cases), and Success Metrics that name the missing instrumentation instead of inventing a target number. |
| [`06-alignment-brief.md`](06-alignment-brief.md) | [`stakeholder-alignment-brief`](../../skills/stakeholder-alignment-brief/SKILL.md) | Originates a cross-functional build-direction decision implied by the spec's own Open Questions/Risks and Rollout Plan, with three real options and a recommendation traceable to their trade-offs. |

## Why file 6 is different from the others

Files 2 through 5 each mechanically apply their skill's process to the previous file's content. File 6 can't work that way — `write-feature-spec`'s own output isn't itself a decision needing stakeholder alignment. So `06-alignment-brief.md` originates a genuine forced-choice question (ship the spec's structured field now, build an AI-generated summary instead, or delay for more data) grounded directly in specifics the spec already surfaced: the adoption risk and unresolved AI-vs-structured question from its Open Questions/Risks, and the pilot sequencing in its Rollout Plan. This is the one place in the chain where a skill adds new decision content rather than reformatting what came before it — which is itself realistic: turning a spec into a decision brief is exactly the kind of judgment call a PM makes once a spec exists, not something a skill should mechanically automate.

## What stays honest throughout, and why it matters

- **Evidence never gets stronger than it earns.** Four thin interviews stay Low confidence through synthesis and opportunity framing; nothing here quietly upgrades to Medium or High to make the chain feel more decisive.
- **A recommendation to slow down is followed by a visible human judgment call, not silently overridden.** `opportunity-framing`'s own recommended next step is "validate further," not "proceed." The intent doc explicitly documents the human decision to proceed anyway, in parallel with validation, rather than pretending the recommendation didn't exist.
- **No invented numbers.** The only concrete reassignment/reopen-rate figures in this entire chain (Vantage Metrics' ~18%/~2x) are flagged, every time they're referenced, as self-reported from memory and not independently verified — they are never laundered into a validated baseline or a success-metric target.
- **Disagreement is reported, not resolved for the reader.** Two interviewees disagree on whether an AI-generated summary or a structured field is the right fix. That disagreement is carried, unresolved, from the research synthesis all the way to the alignment brief's forced choice — it is the decision the brief exists to force, not something an earlier stage should have quietly picked a side on.

## Reading order

Read the files in numeric order — each one names the specific line of the previous file it's building on, so the chain can be followed end to end without cross-referencing anything outside this folder.
