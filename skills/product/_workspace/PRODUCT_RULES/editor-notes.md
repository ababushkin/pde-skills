# Editor notes — PRODUCT_RULES.md

**Verdict:** reject

## Verdict rationale

The draft is structurally complete, citations are intact, and the voice is otherwise correct — but the header contains "operationalises," which is a jargon-as-rigor reject trigger. Additionally, three sentences have been lightly reworded from the source in ways that are not purely formatting changes: Rule A5 drops the (a)/(b) lettering from a paired construction and removes the framing word "anti-pattern"; Rule C3 expands "%" to "percentage"; Rule C5 strips the (a)/(b) labels from the branching conclusion. None of these are serious distortions, but they cross the line from formatting into content editing, and the header word is a hard fail. Fix those four items and this is ready.

## Findings

### Voice and register

Passes. The body is direct and opinionated throughout. No hedging language in the principles or rules sections. Sentence-case headings throughout. No emoji.

### Jargon-as-rigor

**One instance found:**

- Header, line 3: "The companion skill `idea-triage` **operationalises** the problem-framing gate at the point of intake."
  - "Operationalises" is a reject trigger. It substitutes a formal-sounding word for a plain one. Suggested alternatives: "implements," "applies," "runs," "is the skill for" — or rewrite as "The companion skill `idea-triage` handles problem-framing at the point of intake."

No other jargon-as-rigor found in body, rules, or Part 3.

### Header

The header is 4 lines of content (excluding the horizontal rule), within the 3–5 line limit. The structure is correct: states what the file is, names companion artefacts. The single problem is "operationalises" (see above). Remove that word and the header passes.

### Content faithfulness

Three minor rewording changes from the source, none of which involve adding or removing substance:

1. **Rule A5** (draft line 92): Source reads "to prevent the anti-pattern of either (a) inflating trivial work with grand outcomes, or (b) letting real product work escape outcome framing by hiding inside KTLO." Draft reads "to prevent two anti-patterns: inflating trivial work with grand outcomes, or letting real product work escape outcome framing by hiding inside KTLO." The (a)/(b) structure and the word "anti-pattern" are removed. Not a content loss, but it is a wording change beyond formatting. Restore the source wording.

2. **Rule C3** (draft line 139): Source uses "%" throughout; draft expands to "percentage." Not a content change, but inconsistent with source style. Restore "%" as in source.

3. **Rule C5** (draft line 145): Source reads "either (a) a miracle or (b) not being looked at"; draft reads "either a miracle or not being looked at." Labels stripped. Restore the (a)/(b) structure to match source.

**Permitted addition:** The draft adds "The ten principles in one line each:" (lines 188–199) to Part 3. This pattern matches `eng-principles-universal.md` and was listed as an allowed conversion move. All 10 principles are represented accurately and without distortion. No issue.

### Structural completeness

All required sections present and complete:

- **Header:** Present, 4 content lines.
- **Part 1 — Guiding principles:** All 10 principles present with Implication statements. Correct.
- **Part 2 — Laws / Rules:**
  - Area A (what goes on the roadmap): 6 rules (A1–A6). Correct.
  - Area B (prioritisation): 7 rules (B1–B7). Correct.
  - Area C (commitment): 5 rules (C1–C5). Correct.
  - Area D (review and learn): 5 rules (D1–D5). Correct.
- **Part 3 — Quick reference:** Present. Roadmap-is/roadmap-is-not blocks present. Earns-slot and loses-slot lists present. Ten-principles summary added (permitted).
- **Heading case:** All section headings correctly converted to sentence-case from the title-case source.
- **Rule formatting:** Rules correctly bolded in draft; source had them unformatted. Consistent with eng-principles-universal pattern.

### Register match with engineering companion

The draft feels like it comes from the same project. The Part 2 intro paragraph, the rule formatting (bold rule title followed by body), the Implication pattern, and the Part 3 structure all match `eng-principles-universal.md` closely. The citation style (Author's Book Title for framework references, named-person attributions inline) is consistent. Same confidence of voice; same willingness to state opinions without hedging.

## Required changes

1. **Header line 3:** Replace "operationalises" with plain language. Suggested: "The companion skill `idea-triage` handles problem-framing at the point of intake." or "...is the skill for the problem-framing gate at intake."
2. **Rule A5 body:** Restore source wording: "to prevent the anti-pattern of either (a) inflating trivial work with grand outcomes, or (b) letting real product work escape outcome framing by hiding inside KTLO."
3. **Rule C3 body:** Restore "%" symbol in place of "percentage" to match source.
4. **Rule C5 body:** Restore "(a) a miracle or (b) not being looked at" to match source.
