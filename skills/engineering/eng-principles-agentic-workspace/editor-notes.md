# Editor notes — eng-principles-agentic.md

**Verdict:** accept with notes

## Verdict rationale

The draft is structurally sound and mostly meets the bar: all seven principles fail the tier-2 counterfactual test, all seven carry named Implication statements, Part 2 covers the four required amplifications, Part 3 provides a usable quick reference, and the named artefacts (`stop-the-line`, `evidence-claim`, `artefact-pair`) are assigned to correct lifecycle stages. Two issues block clean accept. First, the phrase "gradient-descended toward" in Principle 6 is ML jargon used where a plain statement would serve — this violates the jargon-as-rigor rule. Second, the "~7% drop in delivery throughput" figure cited as a DORA 2024 finding is presented without a chapter or section reference, and the precision (a specific percentage) cannot be verified against the named source — a file whose Principle 2 is "hallucination is the default; sources are the brake" must not carry an unverifiable statistic. Both issues are fixable without structural revision.

## Findings

### Voice and register

Passes on heading case, emoji absence, no hedging language, and citation-bearing prose. Sentence rhythm is good throughout — dense without being turgid. One minor flag: Part 3's framing sentence ("The agentic tier is: an agent's failure modes are predictable…") reads oddly with the colon; it could be a plain declarative. Not a reject trigger but worth tidying.

### Jargon-as-rigor

**Flagged phrase — Principle 6:** "agents are gradient-descended toward 'make the error go away'"

The phrase "gradient-descended" borrows ML training terminology to describe a behavioural tendency. The simple idea is: agents are shaped to produce output that eliminates errors, and silencing an error achieves that goal faster than investigating it. "Gradient-descended" sounds precise but is doing rhetorical work — it signals technical seriousness without adding meaning the plain version lacks. The plain rewrite: "agents are shaped to produce output that resolves errors" or "the easiest path to a green test is deletion, not investigation." This is a reject trigger.

**Borderline — Principle 2:** "statistically reasonable continuations of training data"

Accurately describes how LLM hallucinations arise. Not quite jargon-as-rigor because the phrase does carry information a layperson might not assume (i.e., the fabrications aren't random noise — they're coherent with the training distribution). Flagged for author to consider whether the plain version ("plausible because the model has seen similar code") loses anything material. Not a reject trigger on its own.

### Tier-2 purity

Clean. All seven principles are tested against the counterfactual:

- P1 (context-as-asset): a 2010 engineer has no context window to load. Tier-2.
- P2 (hallucination-as-default): agents fabricate with confidence; humans do not hallucinate APIs. Tier-2.
- P3 (shortest path / spec-as-seatbelt): the specific mechanism named — absence of implicit conversational memory — is agent-specific. Humans carry context from the meeting; agents carry only what is in the file. Tier-2.
- P4 (evidence beats vibes): framed specifically as agents declaring victory at syntax or green tests, whereas human engineers typically seek additional signal. Tier-2.
- P5 (predictable rationalisations): traced to training data reflecting human excuses, and the mechanism (will reach for them when the work gets hard) is agent-specific. Tier-2.
- P6 (stop the line): "agents collapse [the judgement call] almost every time without a hard rule" — the mechanism is agent-specific even though the principle has a universal ancestor. Tier-2.
- P7 (memory in artefacts): explicitly about inter-session discontinuity. Tier-2.

The file correctly acknowledges the universal-tier foundation without duplicating it. Part 2 amplifies four universal principles rather than restating them as new tier-2 principles.

### Part 2 — amplifications

The four named amplifications (small batches, boring technology, review, operability) are the right four. Each maps to a universal principle (8, 10, no single number but embedded across D-rules and review posture, and 1/6 respectively) and the "bites harder" framing is correct — it explains the mechanism of amplification rather than restating the principle.

**Issue — DORA citation specificity:** The small batches amplification cites "the 2024 DORA report's load-bearing finding" and states "a ~7% drop in delivery throughput observed across teams that let batch size grow alongside agent productivity." The report is named specifically (2024 DORA), which meets the "named, not vague" bar for the report itself. However, the ~7% figure is specific enough that a reader would want a chapter or section reference to verify it. A named report with an unverifiable specific statistic is worse than a named report with a directional claim, because it creates the appearance of precision without the substance. The sentence also says "observed across teams" — DORA studies are survey-based; "observed" implies direct measurement. The author should either locate and cite the exact section/page, soften the statistic to a directional finding ("DORA 2024 finds a meaningful drop in delivery throughput"), or remove the percentage if it cannot be pinned to a specific passage. This is a reject trigger on precision grounds given Principle 2's own standard.

The companion finding — "AI-assisted teams that hold batch size constant see the gains compound rather than offset" — is also worth sourcing specifically if it comes from the same DORA report. If it is an inference from the first finding, it should be flagged as such.

### Implication statements

All seven principles carry a named Implication statement. All are actionable. Named artefacts appear where relevant:

- P4 names `evidence-claim` (Next) — correct.
- P6 names `stop-the-line` (Next) — **incorrect lifecycle stage.** Per PROJECT_PLAN §3, `stop-the-line` is a Now item, not Next. The parenthetical says "(Now)" in the draft — re-reading confirms this is actually correct: "the `stop-the-line` hook (Now)." Verified. No error.
- P7 names `artefact-pair` (Later) — consistent with post-v0.1 scope.

One minor issue: P5's Implication says "Every skill includes a 'Common rationalisations' section." This is a strong prescription that creates a cross-artefact requirement. If this is intentional (and it appears to be, as it is the operational form of the principle), it should be acknowledged as binding on all skills in the pack, not just as a recommendation. The draft treats it as definitive, which is correct — no change needed — but the consistency checker should verify that downstream skill artefacts (`design-doc`, `incremental-implementation`) honour it.

### Cross-references

The universal companion (`eng-principles-universal.md`) is named in the opening paragraph and in the tier-2 test statement. The pointer is accurate.

**Gap — Part 3 omits the companion pointer.** The task spec requires Part 3 to contain pointers to the universal companion and to artefacts implementing specific principles. Part 3's final sentence says "Cross-references to universal-tier principles that amplify under agents are in Part 2 above" — this points to Part 2 but does not name `eng-principles-universal.md` explicitly in the quick-reference section. A reader scanning only Part 3 would not know the companion file exists. The fix is a single line: e.g., "Foundation: `eng-principles-universal.md` (tier 1)." Not a reject trigger by itself, but it is an incompleteness against the stated spec.

Named hooks and their lifecycle stages are correctly identified:
- `stop-the-line` — Now. Correct.
- `evidence-claim` — Next. Correct.
- `artefact-pair` — Later. Correct.

## Required changes

1. **Principle 6 — remove "gradient-descended"** (jargon-as-rigor reject trigger). Replace with plain language that conveys the same mechanism: that agents are shaped to produce output that eliminates errors, and suppression achieves that more cheaply than investigation.

2. **Part 2 small batches — resolve the ~7% DORA citation.** Either (a) add the specific chapter/section of the 2024 DORA report that supports the ~7% figure, (b) soften to a directional finding without a specific percentage if the exact passage cannot be located, or (c) remove the percentage and state the finding qualitatively. Do the same for the "gains compound" companion claim if it comes from the same passage.

3. **Part 3 — add explicit pointer to `eng-principles-universal.md`.** One line is sufficient: e.g., "Foundation: `eng-principles-universal.md` (tier 1, ten universal principles)." This makes the quick-reference section self-contained for readers who start there.
