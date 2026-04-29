# Consistency notes — eng-principles-universal.md

**Verdict:** accept

## Verdict rationale

`eng-principles-universal.md` is internally consistent and holds a clean tier-1 boundary against `eng-principles-agentic.md`. No agentic failure-mode language leaks into the universal file; no universally applicable principle is stranded in the agentic file. Cross-references between the two files are present in both directions and accurate. Vocabulary is used consistently across both files and is compatible with the terminology future skills, hooks, and sub-agents will need to cite. One minor path inconsistency in the cross-references is noted but does not warrant a revise verdict because the meaning is unambiguous and the fix is cosmetic. One coverage gap is noted for informational purposes; it is an expected consequence of the roadmap's "principles are embedded, not standalone" design.

---

## Findings

### Tier-1 / tier-2 boundary

Clean.

**Universal file (tier-1 test: would a senior engineer in 2010 agree?)** All ten principles pass the test without exception. Principle 8 ("small batches") cites Reinertsen and Humble & Farley — both pre-AI sources — before referencing DORA, and the DORA reference names the cross-industry deployment-frequency research, not the 2024 AI-productivity finding. The 2024 AI-specific batch-size data is correctly placed in the agentic file (Part 2). Principles 1, 6, 7, and 9 could theoretically import AI flavour, but do not: they are stated entirely in terms of systems, teams, and organisations. No context-window language, no hallucination language, no agent-session-continuity language anywhere in the universal file.

**Agentic file (tier-2 test: would this principle survive without AI coding agents?)** All seven agentic principles fail the counterfactual — they are genuinely agent-specific. Principle 1 (context window as asset) has no human analogue at the same specificity. Principle 2 (hallucination as default) is purely agentic. Principle 3 (shortest path to output is the failure mode) is grounded explicitly in the agent's lack of implicit conversation memory. Principle 5 (pre-rebut rationalisations) has some human-facing precedent in code review culture, but the framing ("these are training data patterns the agent will reach for") is agent-specific. Principle 6 (stop the line) addresses agent gradient-descent toward suppression — agent-specific framing. Principles 4 and 7 are amplifications of universal principles 1 and 6 respectively, but the agentic file is explicit about this and does not duplicate the universal statement.

**Amplification pattern:** The agentic file handles amplification correctly in Part 2. It names four universal principles (8, 10, review-as-practice, 1) that bite harder under agents, explains why, and cites the specific evidence (2024 DORA finding for small batches). None of these amplifications appears in the universal file; they are stated there at the universal level only. The tier boundary is held in both directions.

**One ambiguity worth naming for future authors:** Universal Principle 5 ("code is a liability; YAGNI") and Agentic Principle 3 ("the shortest path is the failure mode; the spec is the seatbelt") overlap in spirit — both argue against producing output prematurely. They are genuinely distinct: one is about scope (don't build what you don't need), the other is about anchoring (don't produce output before the problem is stated). Future skill authors tracing to both should be aware the overlap is intentional and the principles are not duplicates.

### Cross-references

Both files reference each other. The references are accurate on substance. One path issue is noted.

**Universal → agentic:** The opening paragraph names `eng-principles-agentic.md` without a directory prefix. The end of Part 3 repeats this: "see `eng-principles-agentic.md`." Both references list the agentic principles by their exact titles, which is accurate.

**Agentic → universal:** The opening paragraph names `eng-principles-universal.md` without a directory prefix. Agentic Principle 1's implication references "universal Principle 2" by number. Agentic Principle 2's implication references "universal Principle 4" by number. Agentic Principle 4 explicitly names "universal Principle 1 ('shipped is not done; observed is done')." Agentic Principle 7 references "Universal Principle 6's Rule D3" — a specific rule cross-reference, and it is accurate (Rule D3 in the universal file does cover ADR supersession).

**Path issue:** Both files cite each other by filename only, without the `skills/engineering/` path prefix. Per the repo structure in `PROJECT_PLAN.md` §4, both files live at `skills/engineering/eng-principles-universal.md` and `skills/engineering/eng-principles-agentic.md`. Relative references between co-located files in the same directory are unambiguous, so this does not cause confusion. However, future artefacts in other directories (e.g. `skills/engineering/design-doc/SKILL.md`) will need the directory-qualified path when citing these files. The files themselves may want to add a note about their canonical path, or adopt path-qualified self-references. This is informational; not a revise trigger.

**Agentic Part 3 pointer:** The agentic file ends with "Cross-references to universal-tier principles that amplify under agents are in Part 2 above" — this is correct but does not name the companion file explicitly as the universal file's Part 3 pointer does. This is a minor asymmetry; both files are unambiguous on what they are, so no confusion results.

### Vocabulary

The following terms appear with specific meanings that future artefacts must honour consistently.

**"Tier 1 / tier 2"** — The tier split is the structural spine of the engineering principles layer. Both files use "tier 1" to mean universally applicable (human or agent) and "tier 2" to mean agent-specific. This must be propagated consistently. Skills and hooks that trace to principles should name the tier: "traces to Eng Universal Principle 8" or "traces to Eng Agentic Principle 6."

**"Innovation token"** — Used in Universal Principle 10 and Rule B4 to mean the finite budget of technical novelty a team can sustain. The term originates in McKinley's essay. Future artefacts (particularly the `design-doc` skill and `planning-and-task-breakdown` skill) that touch technology adoption should use this exact term rather than synonyms ("budget," "risk allowance," "novelty budget").

**"Fitness function"** — Used in Principle 7 and Rules A5, D4, Part 3 (work-is-complete checklist). Meaning: an automated, continuously running check that an architectural characteristic is holding. Future artefacts must not dilute this to mean "a test" generically. The distinguishing property is continuous and automated, not one-time.

**"Walking skeleton"** — Rule B2, citing Cockburn. Meaning: minimal end-to-end implementation through every real component in the real deployment environment. The `incremental-implementation` skill (Now, item 6) traces to this principle and must use this exact term.

**"Error budget"** — Rule C3, citing Google SRE. Used consistently with the SRE meaning: the allowance for failures within an SLO. The `deploy` skill (Next, item 17) will need to use this term consistently.

**"Blameless postmortem"** — Rule D1. Term is used correctly per Allspaw/Google SRE origin. Any future `incident-review` or `postmortem` skill must match this framing.

**"Blast radius"** — Rules B3 and Part 3. Meaning: how much breaks if a given design decision is wrong. Used once in agentic Principle 6's implication implicitly (the "stop the line" hook fires at PR level). No conflict between the two files; term is used sparingly and consistently.

**"Context window" / "context"** — The agentic file uses "context window" in Principle 1 in the technical sense (tokens in the model's active memory). The universal file does not use this term at all, which is correct. Future artefacts must not use "context" in the LLM-technical sense in tier-1 (universal) files.

**"ADR"** — Used extensively in the universal file (Rules A3, D3) and referenced in the agentic file (Principle 7). Both files use the term consistently per Nygard's definition. The universal file notes ADRs are "immutable once accepted, and superseded rather than edited" — the agentic file echoes this in Principle 7. Consistent.

**Terms used in one file only (no conflict, but flag for awareness):**
- "Tracer bullet" (universal Principle 4) — not used in agentic. No conflict.
- "Inverse Conway Maneuver" (universal Principle 9) — not used in agentic. No conflict.
- "Hallucination" (agentic Principle 2) — correctly absent from universal. Future tier-1 artefacts must not use this term.
- "Rationalisation" (agentic Principle 5) — specifically the agent-training-data pattern sense. Future tier-2 artefacts (skills) must use "rationalisation" in this sense, not in the general psychology sense.

### Coverage gaps

Informational only. Not a revise trigger at this stage.

**Principles with no clear standalone artefact home (expected by design):** Universal Principles 2, 3, 5, 7, 9, and 10 are embedded principles — they appear in the `design-doc` skill, `incremental-implementation` skill, and future rules-checking hooks as embedded gates, red flags, and rebuttal tables. Per `PROJECT_PLAN.md` §1: "most principles end up embedded inside existing skills… a principle earns its own standalone artefact only when it has a workflow, a mechanically-verifiable failure mode, or a structural reason the original agent won't catch its own failure." No gap here; this is the intended pattern.

**Principles with named artefact homes:** Universal Principle 1 (observed-is-done) → `post-launch-impact-review` skill (Next, item 18). Universal Principle 8 (small batches) → `small-batch` hook (Next, item 12). Agentic Principle 6 (stop the line) → `stop-the-line` hook (Now, item 7). These mappings are consistent between the files and the roadmap.

**One gap to note for future authoring:** Universal Rule C8 ("tests are a specification of behaviour, not a coverage metric") has no named artefact home in the Now or Next roadmap. It is likely embedded material for `incremental-implementation` and `design-doc`, but no hook mechanically enforces it. If a `test-quality` hook is considered for Next, this rule is the primary principle it would enforce.

**Agentic Principle 5 ("common rationalisations" section requirement):** The agentic file requires every skill to include a "Common rationalisations" section. No skill exists yet, so the propagation hasn't been validated. The consistency checker flags this as a known forward dependency: the first skill authored (likely `design-doc`) must include this section, and the editor and consistency checker on that artefact must verify it is present.

## Required changes

None.
