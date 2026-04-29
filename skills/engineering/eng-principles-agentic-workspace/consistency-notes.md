# Consistency notes — eng-principles-agentic.md

**Verdict:** accept

## Verdict rationale

The agentic principles file is structurally sound and clean in almost every dimension: the seven principles correctly pass the tier-2 counterfactual test, hook lifecycle assignments (`stop-the-line` Now, `evidence-claim` Next, `artefact-pair` Later) all match PROJECT_PLAN §3 and PROJECT_GOVERNANCE §8.3 exactly, vocabulary is consistent with the companion files, and the product–engineering boundary is clean with no spurious cross-reference needed. One back-reference is wrong: Principle 7 cites "Universal Principle 6's Rule D3" — but Rule D3 (ADRs are living documents) lives under the D-rules section of Part 2 of the universal file, not under universal Principle 6 (Operability, observability, and security are functional requirements). The two have no parent–child relationship; attributing a D-rule to Principle 6 is a factual error in a file whose own standard is that sources be accurate and verifiable.

---

## Findings

### Tier-1 / tier-2 boundary and back-references

All back-references are verified against `eng-principles-universal.md` (rules/eng-principles-universal branch):

| Agentic location | Reference as written | Actual universal content | Verdict |
|---|---|---|---|
| P1 Implication | "universal Principle 2" (spec vs problem) | P2: "Design starts with the problem, not with the stack" | Correct |
| P2 body | "universal Principle 4 (name your assumptions)" | P4: "Assumptions must be named; risky ones must be tested before committing" | Correct |
| P4 body | "universal Principle 1 ('shipped is not done; observed is done')" | P1: "Shipped is not done; observed is done" | Correct — verbatim quote matches |
| P7 body | "Universal Principle 6's Rule D3" | Universal Principle 6 is "Operability, observability, and security are functional requirements." Rule D3 ("ADRs are living documents: re-read, superseded, never quietly ignored") is a standalone rule under Part 2 section D, with no hierarchical relationship to Principle 6. | **Incorrect back-reference** |
| Part 2 — Small batches | "universal Principle 8" | P8: "Small batches beat big batches — every time" | Correct |
| Part 2 — Boring technology | "Universal Principle 10" | P10: "Prefer boring technology; innovation tokens are a scarce resource" | Correct |
| Part 2 — Review | No principle number cited | "Review" is not a numbered universal principle; it appears as Rules section D ("How we review and learn"). The omission of a number is correct — there is no universal Principle to cite. | Correct by omission |
| Part 2 — Operability | "Universal Principle 1 ('shipped is not done; observed is done')" | P1: "Shipped is not done; observed is done" | Correct |

**Finding — P7 back-reference:** The claim "Universal Principle 6's Rule D3 says ADRs are living documents" is incorrect. Rule D3 is not a sub-rule of Principle 6; it is an independent rule in the D-section (How we review and learn). Principle 6 covers operability, observability, and security. The correct citation is simply "Rule D3" or "the universal file's Rule D3," with no association to Principle 6.

### Cross-references to future artefacts

All three hook references were verified against PROJECT_PLAN.md §3 and PROJECT_GOVERNANCE.md §8.3:

- **`stop-the-line` (Now):** Principle 6 Implication names it as "(Now)." PROJECT_PLAN §3 Now table, row 7: `stop-the-line`, category hook, engineering, build/verify. Correct lifecycle stage and category.
- **`evidence-claim` (Next):** Principle 4 Implication names it as "(Next)." PROJECT_PLAN §3 Next table, row 13: `evidence-claim`, category hook, meta, verify. Correct lifecycle stage and category.
- **`artefact-pair` (Later):** Principle 7 Implication names it as "(Later)." PROJECT_GOVERNANCE §8.3 backlog Hook candidates section: "`artefact-pair` (confidence 2) — flag code change without doc/ADR update; depends on artefact discipline being real first." Absent from Now and Next. Correct lifecycle stage.

No misidentifications found.

### Vocabulary consistency

**"Evidence"** — Used consistently across all three files. In `eng-principles-universal.md`, "evidence" is used in architectural and learning contexts (evidence-based deliberation, evidence-based reversals). In `PRODUCT_RULES.md`, it is the central term for prioritisation confidence (Rule B2, ICE scoring, Confidence Meter). In `eng-principles-agentic.md`, it is the term for completion-claim substantiation (Principle 4). All three usages are coherent and non-overlapping in domain. No conflict.

**"Done" / "observed"** — Agentic Principle 4 quotes universal Principle 1 verbatim: "shipped is not done; observed is done." The agentic file correctly scopes its amplification: "applied to the agent's own claims about its work, not just to deployments." Part 2 (Operability) repeats the same quote. `PRODUCT_RULES.md` Rule D4 states "'Done' means the outcome moved, not the feature deployed" — this is the product-domain translation of the same principle, and consistent in intent. Alignment is clean across all three files.

**"Rationalisation"** — Appears only in `eng-principles-agentic.md` (Principle 5 title, body, and Implication). Absent from `eng-principles-universal.md` and `PRODUCT_RULES.md`. This is correct by design: rationalisation-as-agent-failure-mode is a tier-2 concept. However, future skill authors will encounter this term as a required section heading ("Common rationalisations") and must use it consistently. Flag: skill-authoring briefs and `docs/skill-anatomy.md` should name this section format explicitly so all skill authors know it is required and standardised.

**"Context window"** — Appears in agentic Principle 1 as a technical term specific to agent operation. Absent from `eng-principles-universal.md` (confirmed by search — zero results). Correct: this is an agent-specific term and does not appear in the tier-1 file.

### Completeness of 7-principle set

The seven principles together address the known AI-agent failure modes:

1. Context loading → P1 (context-as-asset)
2. Hallucination / fabrication → P2 (sources as brake)
3. Scope drift / speculative solution → P3 (spec as seatbelt)
4. False completion claims → P4 (evidence beats vibes) + `evidence-claim` hook (Next)
5. Trained rationalisation patterns → P5 (pre-rebut them) + Common rationalisations section in skills
6. Signal suppression → P6 (stop the line) + `stop-the-line` hook (Now)
7. Inter-session amnesia → P7 (memory in artefacts) + `artefact-pair` hook (Later)

No failure mode is named in the principles without at least a directional implementation path (embedded skill constraint, hook, or sub-agent). The `artefact-pair` gap (P7) is explicitly accepted as Later by design. The "Common rationalisations" section (P5) has no mechanical hook, but the Implication makes the implementation path clear: it is embedded in every skill directly, which is appropriate given the prescriptive nature of P5.

No gaps or overlaps found across the seven principles.

### Product file alignment

`PRODUCT_RULES.md` Rule B2 (ICE scoring with Confidence Meter) and agentic Principle 4 (evidence beats vibes) both invoke the concept of evidence-over-opinion. However, they operate in distinct domains: product Rule B2 governs evidence for prioritisation decisions (is this idea worth building?); agentic Principle 4 governs evidence for completion claims (has the work done what it was meant to do?). The shared vocabulary ("evidence") is used consistently, the use cases are non-overlapping, and no cross-reference is needed. The division is clean.

No other interactions between PRODUCT_RULES.md and the seven agentic principles require annotation.

---

## Required changes

1. **Principle 7 body — correct the back-reference.** Replace "Universal Principle 6's Rule D3 says ADRs are living documents that get superseded rather than ignored" with a reference that does not attribute Rule D3 to Principle 6. Suggested fix: "The universal file's Rule D3 says ADRs are living documents that get superseded rather than ignored." Alternatively: "Rule D3 in `eng-principles-universal.md` says ADRs are living documents that get superseded rather than ignored." The key correction is removal of "Principle 6's" — Rule D3 is a standalone D-section rule, not a sub-item of any numbered principle.

## Confirmation pass (v3)

**Verdict:** accept

Citation corrected. No new inconsistencies introduced.
