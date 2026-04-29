# Editor notes — eng-principles-universal.md

**Verdict:** accept

## Verdict rationale

The draft is structurally complete, tonally sound, and tier-1 clean. All ten principles are present with named implications. The four Part 2 rule areas are present and fully numbered. The quick reference is present and faithfully compresses the principles. No agentic content has leaked in. Citations are specific and named throughout. One phrase qualifies as jargon-as-rigor and must be fixed. Two additional notes — one on an implication phrase and one on a rule word choice — are minor but worth correcting before the consistency check. No reject triggers fire.

---

## Findings

### Voice and register

Passes overall. The register is direct, dense, and opinionated throughout. Headings are sentence-case. No emoji. Prose is used where prose works; bullets appear only in the quick reference where enumeration is appropriate.

One sentence in Principle 4's body is longer than it needs to be:

> "Hunt & Thomas's *The Pragmatic Programmer* prescribes tracer bullets: real code that exercises the riskiest path early, to discover what you don't know."

The sentence works but the trailing clause ("to discover what you don't know") is filler — the tracer-bullet definition already implies it. Suggestion: cut the trailing clause. Minor; not a reject trigger.

### Jargon-as-rigor

One instance found.

**Principle 4, implication:** "…identify the three riskiest assumptions and **discharge them** with a time-boxed spike."

"Discharge" is the failure mode from `docs/authoring-learnings.md` §4 — it is cited explicitly there as jargon-as-rigor ("discharge the assumption" → "test the assumption"). The word sounds rigorous but the idea is simple: test the assumption. Use "test them" or "validate them."

No other instances found.

### Content quality

**Citations:** Named and specific throughout. DORA, Reinertsen, Humble & Farley, Fowler, Beck, Nygard, Cockburn, Skelton & Pais, McKinley, Larson, Conway — all cited by name and source. No vague appeals to authority. Principle 7 cites Ford/Parsons/Kua; Principle 9 cites Evans for DDD. This is the citation density the voice spec calls for.

**Implications:** All ten are present and named. All are operational and checkable. Principle 3's implication ("name (a) whether it's reversible and (b) how expensive the reversal is") is slightly more awkward in prose than the others due to the inline lettering. Not a reject trigger, but the author may want to smooth it.

**Rule operationality:** Rules are consistently checkable. A team member can verify A1 (trigger list), A4 (numbers not adjectives), C4 (red build is top priority), D4 (four DORA metrics named). Rule B6 introduces a minor terminology shift — "Rule of Three; Fowler" — where the citation for the Rule of Three is Fowler but the principle is more commonly attributed to Beck/Jeffries from XP. Fowler popularised it in *Refactoring* (1999), so the citation is defensible, but noting it here for the author's awareness.

**No duplicate coverage between principles and rules:** The rules in each section add operational specificity — they do not merely restate the principle above them. A1–A7 operationalise Principles 2, 3, 4, and 6. C1–C9 operationalise Principles 1, 6, 7, and 8. The no-redundancy bar is met.

### Structural completeness

All required parts present:

- **Part 1:** 10 principles, each with a named "Implication:" block. Complete.
- **Part 2:** Four lettered areas — A (specifications, rules A1–A7), B (design, rules B1–B7), C (build/ship, rules C1–C9), D (review/learn, rules D1–D7). All present and numbered.
- **Part 3:** Quick reference present. The "work earns its slot / work is complete" checklist is a useful addition beyond the ten-line summary. The ten-principle summary faithfully compresses the original titles.
- **Pointer to agentic companion:** Present at the end of Part 3, naming specific agentic principles by their titles. Well-executed.

The opening section (before Part 1) correctly scopes the tier split and names the companion file. The overlap handling note ("When the two tiers overlap…") is clear and correct.

### Tier-1 purity

Clean. No context-window language, no hallucination language, no agent-completion-claim language, no AI-specific failure modes. The principles are stated in terms that a senior engineer in 2010 would recognise and agree with. Principle 8 ("small batches") references DORA research but grounds the claim in Reinertsen (economics) and Humble & Farley (continuous delivery) before citing DORA — both pre-AI sources. The DORA citation in Principle 8 refers to the cross-industry deployment-performance research, not to the 2024 AI-specific finding (that lives correctly in the agentic file). Clean split.

---

## Required changes

1. **Fix jargon-as-rigor in Principle 4 implication.** Replace "discharge them with a time-boxed spike" with "test them with a time-boxed spike" (or "validate them"). This is the only change required before the consistency check.

2. (Optional, author's discretion) Trim trailing clause in Principle 4 body: "…to discover what you don't know" adds nothing. Cutting it tightens the sentence.

3. (Optional, author's discretion) Smooth the inline lettering in Principle 3's implication: "(a) whether it's reversible and (b) how expensive the reversal is" reads slightly more as a list than the prose style of other implications. A recast like "name whether it's reversible and how expensive the reversal is" flows better.

---

## Confirmation pass

**Verdict:** accept

Both changes correctly applied. The Principle 4 implication now reads "test them with a time-boxed spike" — the jargon-as-rigor fix is in place and the wording is clean. The tracer-bullets sentence in the Principle 4 body ends at "real code that exercises the riskiest path early" with the trailing clause removed, tightening the sentence without any loss of meaning. No other content changed. Ready for consistency check.
