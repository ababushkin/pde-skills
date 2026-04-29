```yaml
artefact: idea-triage
category: skill
pack: product
roadmap_position: now
lifecycle_stage: define
length_target: 200–280
predecessor:
  repo: https://github.com/addyosmani/agent-skills
  skill: idea-refine
  relation: adjacent
  url: https://github.com/addyosmani/agent-skills/blob/main/idea-refine/SKILL.md
prior_art_notes:
  read_first:
    - skills/product/PRODUCT_RULES.md
    - agent-skills/idea-refine/SKILL.md (addy's predecessor)
    - references/confidence-meter.md (when authored)
    - references/ice-scoring.md (when authored)
  keep: >
    Structured intake discipline — the instinct to slow down and interrogate an idea before
    acting on it. addy's skill correctly identifies that raw ideas need interrogation before
    they can do useful work. That posture carries over.
  change: >
    Scope is narrower: single-idea triage, not multi-round refinement. Where idea-refine is
    an iterative, open-ended refinement loop, this skill is a gate — it runs once, produces a
    structured record, and routes the idea to the right place (idea bank, validation slot, or
    immediate roadmap consideration). Confidence scoring (Gilad's ICE) is a required output,
    not optional enrichment. PRODUCT_RULES vocabulary throughout (P2, P3, P4, A2, A6, B2, B6).
    "When not to use" explicitly names KTLO/compliance/partner-obligation items (Rule A5
    carve-out) — those skip this gate entirely.
  do_not_copy: >
    No paragraphs copied verbatim from idea-refine. Author reads it as input and authors fresh.
principles_implemented:
  - source: product
    id: P2
    bucket: embedded
    note: Gate checks whether the idea is framed as a problem or a solution; rewrite is required before the idea can proceed.
  - source: product
    id: P3
    bucket: embedded
    note: Output record explicitly labels the idea as a bet with a stated confidence score, not a commitment.
  - source: product
    id: P4
    bucket: embedded
    note: Confidence score is mandatory on every triage record; opinion-only evidence is named and flagged, not silently accepted.
  - source: product
    id: A2
    bucket: embedded
    note: Triage record template requires problem, customer segment, and expected outcome — the three A2 fields — or the record is incomplete.
  - source: product
    id: A6
    bucket: embedded
    note: Skill routes every triaged idea to exactly one of two places — idea bank or roadmap consideration — parking-lot routing is an explicit failure mode.
  - source: product
    id: B2
    bucket: embedded
    note: ICE score with explicit Confidence component is a required output field on the triage record.
  - source: product
    id: B6
    bucket: embedded
    note: Skill's routing logic enforces low-confidence → validation slot, not build slot; this is surfaced as a hard gate, not a suggestion.
triage_record_ref: "PROJECT_PLAN.md §11.1, row #2 — confidence 7, evidence: strong principle backing; v0.1 scoping demonstrated need"
purpose: >
  idea-triage is the intake gate for the product system. It fires when an idea arrives in any
  form — verbal, written, issue, customer request, competitive observation — and its sole job
  is to answer three questions before that idea goes anywhere: Is it framed as a problem or a
  solution? Is there evidence, and how much? Is the problem worth pursuing at all? The skill
  produces a structured triage record — not a refined idea, not a spec, not a decision — and
  routes that record to either the idea bank or immediate roadmap consideration based on
  confidence. It is the mechanism by which PRODUCT_RULES P2, P3, P4, A2, A6, B2, and B6 get
  applied at the moment an idea first enters the system, before any solution thinking begins.
scope:
  in: >
    Single-idea intake. Problem-or-solution diagnosis. Evidence interrogation. Confidence
    scoring (ICE with explicit Confidence). Problem restatement when the idea arrives as a
    solution. Routing to idea bank or roadmap consideration. Production of a structured triage
    record conforming to the A2 template (problem / customer / outcome).
  out: >
    Prioritising the idea against other ideas — that is roadmap-shape territory (Next item #11,
    not yet authored). Multi-round refinement of the idea — that is addy's idea-refine pattern,
    which this skill deliberately narrows. Solution design or scoping — that belongs in
    design-doc. Deciding whether the idea enters the Now roadmap — that is a separate judgment
    made by the team or product owner against current capacity and strategic context.
    KTLO/compliance/partner-obligation work — Rule A5 carve-out; those items skip this gate
    entirely and go straight to backlog.
size_triggers:
  fires_for: >
    Any idea that arrives from outside the existing roadmap and backlog: user request, stakeholder
    suggestion, customer feedback, competitive observation, internal brainstorm output, opportunistic
    observation in analytics. Fires regardless of idea size — the triage step is cheap; the cost
    of skipping it is not.
  does_not_fire_for: >
    KTLO work: bug fixes, compliance items, partner obligations, minor maintenance (Rule A5).
    Work already on the roadmap that is being refined or scoped — that is design-doc or
    incremental-implementation territory. Ideas that have already passed triage and hold a
    confidence score — re-triage only if material new evidence arrives that changes the score.
inputs: >
  The raw idea, in whatever form it arrived: a sentence, a Slack message, a customer quote,
  a feature request, a competitor announcement, an analytics anomaly. No special format required
  at intake. The skill works with whatever text is provided and interrogates it from there.
outputs:
  artefact_path: docs/idea-bank/<idea-slug>.md
  artefact_name: "<idea-slug>-triage.md or an entry in idea-bank/<idea-slug>.md"
workflow_outline: >
  1. Receive the raw idea. Capture it verbatim — no interpretation yet.
  2. [GATE] Diagnosis: is this a solution or a problem? If solution, restate as the underlying
     problem before proceeding. If the underlying problem cannot be articulated, the idea is
     not ready for triage — return to the submitter for clarification.
  3. Interrogate evidence: who is affected, how often, what is the observable negative outcome?
     Assign a Confidence score using Gilad's Confidence Meter (opinion = 0.1, anecdote = 0.5,
     survey/market data = 2–5, experiment/smoke test = 5–8, validated launch = 8–10).
  4. Apply the A2 template: write the problem statement in the form "For [customer segment],
     we believe [problem] is causing [negative outcome]."
  5. [GATE] Does the problem statement hold? If the team cannot agree on the customer, the
     problem, or the negative outcome, the idea is not ready. Return for clarification or discard.
  6. Score ICE: assign Impact (1–10), Confidence (from step 3, scaled 1–10), Ease (1–10).
     Compute ICE = I × C × E. Note: Ease is an estimate only; do not over-invest in it at
     triage stage.
  7. [GATE] Routing: if Confidence < threshold (default: below 5 on the Gilad scale), route to
     validation slot — do not assign a build bet. If Confidence ≥ threshold, route to idea bank
     as a candidate for roadmap consideration. There is no parking lot (Rule A6).
  8. Write the triage record and file it.
artefact_template: |
  # Triage record: <idea-slug>

  ## Raw intake
  <!-- Verbatim capture of the idea as received. Do not edit. -->

  ## Problem restatement
  <!-- "For [customer segment], we believe [problem] is causing [negative outcome]." -->
  <!-- If the idea arrived as a solution, record the original solution framing here and
       explain the restatement. -->

  ## Evidence
  <!-- What evidence exists that this problem is real and affects the named customer?
       Be specific: quote, data point, observation. Name the source. -->
  <!-- Confidence score (Gilad): [0.1–10] — state the evidence type that drives this score. -->

  ## ICE score
  | Dimension  | Score (1–10) | Rationale                  |
  |------------|-------------|----------------------------|
  | Impact     |             | <!-- expected magnitude --> |
  | Confidence |             | <!-- evidence quality -->   |
  | Ease       |             | <!-- rough effort proxy --> |
  | **ICE**    | **= I×C×E** |                            |

  ## Routing
  <!-- idea bank | validation slot -->
  <!-- State the routing and the reason. If validation slot: name the type of validation
       work needed to raise confidence (customer interview, smoke test, experiment, etc.). -->

  ## Notes
  <!-- Anything the author needs a future reader to know: related items in the idea bank,
       strategic context that influenced the score, assumptions baked into the evidence
       assessment. -->
common_rationalisations: |
  | Rationalisation | Rebuttal |
  |---|---|
  | "We know the customer wants this — no need to score it low." | An assertion about customer want is an anecdote (0.5) until there is data. Score it honestly and let the routing logic decide. |
  | "It's a small idea, triage is overkill." | Triage is a 10-minute gate. Skipping it is how small ideas accumulate into a roadmap nobody believes in. |
  | "The CEO asked for it, so the confidence is high." | CEO opinion is 0.1 on the Confidence Meter. That is the whole point of Rule B2. Route it to validation like anything else at that confidence level. |
  | "We can just put it in a parking lot for now." | Rule A6: there is no parking lot. The idea bank is the only holding area for unvalidated hypotheses. |
  | "It's clearly a problem framing, we don't need to write it out." | If it's clear, writing it out takes two minutes. If it takes more than two minutes, it wasn't as clear as assumed. |
  | "Low confidence just means we need to build and see." | That is a build bet on an unvalidated hypothesis. Rule B6: low confidence earns a validation slot, not a build slot. |
  | "This is a bug fix / compliance item — does it need triage?" | No. Rule A5 carve-out: KTLO work goes straight to backlog. This is exactly the "when not to use" case. |
references: |
  - PRODUCT_RULES.md — P2, P3, P4, A2, A5, A6, B2, B6 (direct trace)
  - references/confidence-meter.md — Gilad's Confidence Meter calibration scale
  - references/ice-scoring.md — ICE scoring mechanics and worked examples
  - Itamar Gilad, "GIST Planning" and "Confidence Meter" (external)
  - Marty Cagan, "Inspired" — problem-vs-solution framing, SVPG
  - Janna Bastow, Now-Next-Later roadmap — A6 idea bank / roadmap distinction
dependencies:
  prerequisite_artefacts:
    - skills/product/PRODUCT_RULES.md (must be authored first — vocabulary source)
  invokes:
    - references/confidence-meter.md (confidence scoring)
    - references/ice-scoring.md (ICE mechanics)
  invoked_by:
    - roadmap-shape (Next #11) — idea-triage produces the records that roadmap-shape operates on
authoring_notes: |
  - The skill does NOT prioritise ideas against each other. Any step that compares this idea
    to other ideas is out of scope. That is roadmap-shape. If the author finds themselves
    writing comparative logic, stop and move it to a "see also" note pointing at roadmap-shape.
  - The confidence score is a required output field, not optional enrichment. The artefact
    template must make this impossible to skip.
  - "When not to use" must name KTLO/compliance/partner-obligation items explicitly (Rule A5).
    The author should also name the addy idea-refine skill as the right tool for open-ended
    iterative refinement — this skill is the gate, not the loop.
  - Distinguish this skill from addy's idea-refine clearly in the frontmatter fields
    kept_from_predecessor and changed_from_predecessor. The editor will verify this.
  - The routing gate (step 7) must be written as a hard gate, not a suggestion. "Consider
    validation" is not acceptable. "Route to validation slot" is.
  - Prose over bullets where prose works. The workflow steps should read as executable
    instructions, not as a checklist of vague activities.
  - Voice: direct, dense, no hedging. Match PRODUCT_RULES.md register. No jargon-as-rigor —
    if "structured problem articulation" appears in the draft, replace it with "writing the
    problem down."
  - Length target 200–280 lines. The artefact template and the rationalisations table will
    consume a significant portion; the workflow and purpose sections should be tight.
  - references/confidence-meter.md and references/ice-scoring.md may not be authored yet
    when this skill is written. The author writes the skill against their expected content
    and links them; the consistency checker verifies the links are coherent once they exist.
```
