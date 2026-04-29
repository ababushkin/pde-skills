# Consistency notes — PRODUCT_RULES.md

**Verdict:** accept

## Verdict rationale

PRODUCT_RULES.md is consistent with eng-principles-universal.md in all substantive respects. The two files share the same structural idiom, the same voice, and — critically — the same foundational commitments on definition of done, evidence over opinion, and outcome orientation. There are no contradictions between the files. One minor cross-reference asymmetry exists in the header (see below), and three shared terms are used compatibly but with different disciplinary framings that future authors should understand; neither rises to a required change. The file is ready for owner sign-off.

## Findings

### Relationship with engineering principles

**Definition of done.** Product P10 ("Done means the outcome moved, not the feature shipped") and Rule D4 ("Done is outcome achieved, not feature deployed") map cleanly onto engineering P1 ("Shipped is not done; observed is done"). The product side frames done as outcome-metric movement; the engineering side frames done as production telemetry observed and metric movement confirmed. These are the same principle stated from different roles: the product file owns the "did the outcome move?" question; the engineering file owns the "is it actually running and observable in production?" question. The definitions are complementary, not redundant, and together they close the loop.

**Evidence beats opinion.** Product P4 uses Gilad's Confidence Meter to make the evidence-vs-opinion distinction concrete for prioritisation decisions. Engineering P4 ("Assumptions must be named; risky ones must be tested before committing") makes the same distinction concrete for design decisions. The product formulation quantifies confidence (0.1 for CEO opinion, 0.5 for anecdote, higher for experimental data); the engineering formulation prescribes the method for discharging risk (tracer bullets, time-boxed spikes). These are aligned in spirit and complementary in scope: product governs when to commit to a bet; engineering governs how to test the technical assumptions within that bet.

**No contradictions found.** No product principle contradicts an engineering principle. The product file appropriately defers all implementation-approach and system-design decisions to engineering — "Solution detail is allowed in working documents (pitches, briefs, design explorations) but is not the roadmap itself" (Rule A4) is the clearest expression of this deference.

**Engineering cross-references in the product file.** Rule B2's "Ease is an effort estimate from engineering/design" and Rule C4's "platform capability" and "cross-team dependencies" language are the only places the product file directly references engineering concerns. Both are appropriate: ease of implementation is a legitimate product-side input to prioritisation (it appears in ICE scoring), and surfacing cross-team dependencies before commitment mirrors engineering Rule B7. There are no gratuitous engineering details.

### Boundary clarity

**What product covers that engineering does not:** roadmap structure (Now/Next/Later horizons, Rule A1), problem framing vs. solution framing at the roadmap level (P2, Rule A4), outcome-based success criteria (Rule A3), portfolio theme classification (Rule B3), Kano classification (Rule B4), appetite-setting as a product commitment (Rule C1), high-integrity commitment discipline (Rule C2), explicit capacity allocation across themes (Rule C3), PM-led impact review and decision retrospective (Rules D1, D3, D5). None of this territory is in the engineering file.

**What engineering covers that product does not:** design doc and ADR discipline, technical risk management, build mechanics (trunk-based development, CI, feature flags, error budgets), system architecture principles (Conway's Law, evolutionary architecture, boring technology), team topology, and operational maturity. None of this territory appears in the product file.

**No leaks detected.** The product file contains no guidance on implementation approach, system design, build/ship mechanics, technical tooling, or operational practice. Rule C1's "appetite" concept (how much time a problem is worth) is product-level scope management, not engineering estimation — it is correctly placed. Rule C4's dependency identification is a planning concern, not an engineering execution concern.

**Minor overlap zone (informational).** Both files reference "cost of delay" as a sequencing concept: product Rule B5 uses it for roadmap prioritisation; engineering P8 (small batches) is underpinned by Reinertsen's same concept. The product file cites Reinertsen via Perri; the engineering file cites Reinertsen directly. The usage is consistent and the overlap is productive rather than duplicative.

### Vocabulary

**"Outcomes."** Used consistently in both files. Product: outcomes as the measure of roadmap success (P1, P10, Rules A2, A3, D4). Engineering: "outcome achieved" in the Part 3 definition of done and in D2 ("did the target metric move"). Usage is identical in meaning.

**"Evidence."** Used consistently. Product: evidence as the basis for confidence scoring (P4, Rule B2, Rule B6). Engineering: evidence as what a spike or tracer bullet produces (P4, Rule C5). Same word, same meaning, different contexts (pre-bet vs. during-build).

**"Confidence."** Product file uses Gilad's Confidence Meter with an explicit numeric scale; engineering file does not use "confidence" as a term of art but refers to the same concept via "named assumptions" and "time-boxed spikes." The product file has the more operationalised definition. No inconsistency, but future authors should know that "confidence" in the product context carries the specific Gilad numeric framing, while the same concept in the engineering context is expressed as assumption-testing discipline.

**"Done."** Covered above under "Definition of done." Used consistently across both files.

**"Appetite."** Appears in product file (P8, Rules C1, C3) as the time budget for a roadmap item. Does not appear in the engineering file, which refers to "time-box" for spikes (Rule C5) and "short-lived branches" for batches (Rule C1). These are compatible but distinct: appetite is the product-side budget-setting act; time-boxing is the engineering-side execution constraint. No vocabulary clash.

**"Small batch."** The term does not appear in PRODUCT_RULES.md. Engineering P8 is "Small batches beat big batches." The product file's closest equivalent is P8's appetite discipline (fixed time, variable scope), which produces small batches as a side effect but does not name the principle. This is not an inconsistency — the two principles are about different levels of granularity — but future authors of downstream product skills may want to explicitly acknowledge engineering P8 as the delivery-level companion to the product-side appetite principle.

**"Discovery" and "validation."** Both terms appear in the product file (discovery work in Rules B6, C2, C3; validation in Rules A6, B6). Neither appears as a named concept in the engineering file, which covers the same territory under "spike" (Rule C5) and "tracer bullet / walking skeleton" (P4, Rule B2). The product file's "validation slot" and the engineering file's "spike" are equivalent concepts at different abstraction levels. Compatible; no clash.

### Cross-references

**`idea-triage`.** Described in the header as "The companion skill `idea-triage` handles problem-framing at the point of intake." PROJECT_STATE.md lists `idea-triage` as item #2 in the Now tier. The description is accurate: `idea-triage` is a skill (correct category) and its scope — problem-framing at intake — is consistent with what the product file implies it does (triage incoming ideas before they reach the roadmap). The header does not label it "(Now)" while it does label `roadmap-shape` as "(Next)." This asymmetry is minor but creates an inconsistent reader experience: a reader who knows to look for horizon tags will notice the omission. Suggested fix (optional, not blocking): add "(Now)" to the `idea-triage` reference to match the pattern set by `roadmap-shape`.

**`roadmap-shape`.** Described as "`roadmap-shape` (Next) covers the mechanics of building and maintaining the roadmap itself." PROJECT_STATE.md lists `roadmap-shape` as item #11 in the Next tier. Description is accurate: it is a skill, it is a Next artefact, and its described scope (roadmap mechanics) is consistent with the product file's own scope (which covers principles and rules but explicitly defers the mechanics of roadmap construction to `roadmap-shape`).

**No references to non-existent artefacts.** The two companion artefacts named in the header both exist in PROJECT_STATE.md with the correct category and scope. No other external artefacts are referenced.

### Coverage gaps

Looking at the ten product principles for future skill/hook/sub-agent homes:

1. **P1 (Outcomes, not outputs)** — `post-launch-impact-review` skill (Next, item #18) is the natural home. Well covered.
2. **P2 (Items are problems to solve)** — `idea-triage` (Now, item #2) handles this at intake. Well covered.
3. **P3 (Every item is a bet)** — No single dedicated artefact yet, but the betting-table framing will likely live in `roadmap-shape` (Next). Plausible home exists.
4. **P4 (Evidence beats opinion)** — `idea-triage` + `references/confidence-meter.md` + `references/ice-scoring.md`. Well covered.
5. **P5 (Focus is the multiplier)** — `roadmap-shape` or a future `roadmap-review` skill (Next, item #19). Plausible home exists.
6. **P6 (Value flows both ways)** — No dedicated artefact in Now or Next. The four-risk framework (Cagan) is referenced in Rule B1 but no skill operationalises the viability check. Informational gap only — this could be a useful `viability-check` hook or sub-agent in a later cycle.
7. **P7 (Certainty decays with time horizon)** — `roadmap-shape` is the natural home for Now/Next/Later mechanics. Well covered.
8. **P8 (Fixed time, variable scope)** — appetite discipline likely lives in `roadmap-shape`. Plausible home exists.
9. **P9 (Strategic context matters more)** — No artefact in Now/Next handles product strategy upstream of the roadmap. This is the largest coverage gap in the v0.1 pack: the strategy-to-roadmap connection is asserted as a principle (P9) but no skill, hook, or sub-agent helps a PM do it. Informational; out of scope for this file to address.
10. **P10 ("Done" means outcome moved)** — `post-launch-impact-review` (Next, item #18) is the direct home. Well covered.

## Required changes

None.
