artefact: design-doc
category: skill
pack: engineering
roadmap_position: now
lifecycle_stage: define
length_target: 250–300 lines
predecessor:
  repo: https://github.com/addyosmani/agent-skills
  skill: spec-driven-development
  relation: derivative
  url: https://github.com/addyosmani/agent-skills/blob/main/skills/spec-driven-development/SKILL.md
prior_art_notes:
  read_first:
    - skills/engineering/eng-principles-universal.md (Rules A1, A2, A4, A5, A6, B2, B3)
    - skills/engineering/eng-principles-agentic.md (Principles 1, 3)
    - addy's spec-driven-development skill (predecessor, read before drafting)
  keep: >
    The premise that a written spec must precede any implementation. The structured
    intake discipline — capturing the problem before solution language appears. The
    principle that reviewing a document is cheaper than reviewing code built on a
    misunderstood problem.
  change: >
    1. Structure is now anchored to a specific format from Rule A2 (Problem → Context →
    Constraints → Alternatives → Recommended approach → Consequences → Operability plan
    → Open questions), derived from Nygard/Larson, not left to author discretion.
    2. Rule A1 supplies three explicit trigger conditions that govern when a design doc
    is required versus an ADR.
    3. Walking skeleton (Rule B2) is a named, required gate before implementation detail
    is filled in — not mentioned in addy's skill.
    4. Operability section (Rule A6) is a hard reject condition, not an optional section.
    5. "Common rationalisations" section is required by Agentic Principle 5 and must name
    the three most common bypasses the agent will attempt.
    6. "When not to use" explicitly names the right alternatives — ADR for sub-threshold
    decisions; spike (Next) for exploratory unknowns.
  do_not_copy: >
    No paragraph from addy's skill is reproduced verbatim. Structure may share intent;
    voice and prose must be re-authored from scratch to match the owner's register.
principles_implemented:
  - source: eng-universal
    id: P2
    bucket: standalone
    note: >
      The skill IS the operational form of this principle — it enforces problem-first
      structure through the mandatory A2 document template and makes solution-first
      approaches structurally impossible to complete.
  - source: eng-universal
    id: Rule A1
    bucket: embedded
    note: >
      Three trigger conditions (4+ weeks, reused capability, meaningful user/cost/
      compliance impact) determine when a design doc is required; embedded in the
      "When to use" section and enforced as a gate before the workflow begins.
  - source: eng-universal
    id: Rule A2
    bucket: standalone
    note: >
      The seven-section structure (Problem → Context → Constraints → Alternatives →
      Recommended approach → Consequences → Operability plan) is the non-negotiable
      skeleton the artefact template produces; every section is mandatory.
  - source: eng-universal
    id: Rule A4
    bucket: embedded
    note: >
      NFRs must appear with numbers in the Constraints section; "fast," "reliable," and
      "scalable" are rejected — enforced as a gate on the Constraints section.
  - source: eng-universal
    id: Rule A5
    bucket: embedded
    note: >
      Fitness functions are required alongside NFR targets; embedded as a named sub-item
      in the Constraints section guidance.
  - source: eng-universal
    id: Rule A6
    bucket: embedded
    note: >
      Operability section is required in every design doc; its absence is named as a
      reject trigger in "Red flags" and in the verification criteria.
  - source: eng-universal
    id: Rule B2
    bucket: embedded
    note: >
      Walking skeleton recommendation is a named workflow gate: the skill instructs the
      author to plan a minimal end-to-end path before filling in implementation detail,
      and to note it explicitly in the Consequences section.
  - source: eng-universal
    id: Rule B3
    bucket: embedded
    note: >
      Every Alternatives section must name blast radius and reversibility cost for each
      option; embedded as a required field in the Alternatives section guidance.
  - source: eng-agentic
    id: P1
    bucket: embedded
    note: >
      Skill names exactly which files and prior decisions to load before starting —
      enforcing the "context is the asset" principle rather than letting the agent
      decide what to read.
  - source: eng-agentic
    id: P3
    bucket: embedded
    note: >
      Skill explicitly forbids solution language until the Problem section is drafted and
      acknowledged; the spec is named as the mechanism that holds the work to the actual
      task.
triage_record_ref: PROJECT_PLAN.md §11.1 row #5
purpose: >
  design-doc teaches an agent (or engineer) to produce a structured design document
  before any non-trivial implementation begins. It is the operational form of universal
  Principle 2 (design starts with the problem, not the stack): the skill enforces
  problem-first thinking by making the document structure itself the constraint — an
  agent cannot complete the artefact without working through Problem, Context,
  Constraints, Alternatives, and Operability in that order. The skill governs when a
  design doc is required (Rule A1 trigger conditions), what structure it must follow
  (Rule A2), and what sections are hard rejections when absent (Rule A6). It does not
  produce implementation code; it produces the document that reviewers evaluate before
  any code is written.
scope:
  in: >
    Writing or reviewing a design document for non-trivial work that meets at least one
    Rule A1 trigger. Determining whether a trigger applies. Following and populating the
    Rule A2 structure. Recommending a walking skeleton as the first build step. Naming
    NFRs with numbers and fitness functions. Completing the Operability section.
  out: >
    Architecturally significant decision records for sub-threshold work — that is the
    ADR pattern (Rule A3); this skill does not author ADRs. Exploratory technical
    investigation where the problem is unknown — that is `spike` (Next). Implementation
    itself — the skill hands off to `incremental-implementation` once the design doc is
    accepted. Post-launch review of whether the design held — that is
    `post-launch-impact-review` (Next).
size_triggers:
  fires_for: >
    Work meeting at least one of: (1) more than four weeks of estimated engineering time;
    (2) the capability built will be used by parties outside the team building it; (3)
    the change has meaningful impact on users, operational cost, or compliance posture.
    Any one of the three is sufficient.
  does_not_fire_for: >
    Sub-threshold work that meets none of the three triggers above — write a short ADR
    instead (Rule A3). Exploratory unknowns where the problem itself is not yet
    understood — run a `spike` first (Next), then return to this skill. Changes that are
    purely additive and clearly reversible with no shared-interface surface — these may
    go directly to `incremental-implementation`.
inputs: >
  A problem description or feature request, however rough. Any known constraints
  (functional and non-functional). Named stakeholders or affected users. A rough scope
  estimate that suggests the Rule A1 trigger conditions are met. Prior design docs or
  ADRs for related capabilities (loaded per Agentic Principle 1). Access to the relevant
  sections of eng-principles-universal.md (Rules A1, A2, A4, A5, A6, B2, B3).
outputs:
  artefact_path: docs/design-docs/<kebab-case-name>/design-doc.md
  artefact_name: design-doc.md
workflow_outline: |
  1. TRIGGER CHECK [GATE] — verify at least one Rule A1 condition holds. If none hold,
     stop and recommend an ADR. If the problem is not yet understood, stop and recommend
     a spike.
  2. CONTEXT LOAD — load prior design docs, ADRs, and principles relevant to this
     problem space (Agentic P1). Name what was loaded.
  3. PROBLEM SECTION — draft the Problem section first. No solution language appears
     until the problem is stated, the affected users are named, and the current behaviour
     vs. desired behaviour is made explicit. [GATE]: problem is acknowledged before
     proceeding.
  4. CONTEXT AND CONSTRAINTS — document background, history, and known constraints.
     NFRs must appear with numbers and units (Rule A4). Each NFR must name its fitness
     function — the automated check that will verify it (Rule A5).
  5. ALTERNATIVES — list at least two alternatives considered, including the "do
     nothing" option. For each, name: blast radius if this option is wrong, and reversal
     cost (Rule B3). A design doc with only the chosen approach in the Alternatives
     section is incomplete.
  6. RECOMMENDED APPROACH — state the recommendation. Explain why it beats the
     alternatives on the named constraints. This section is last because the problem
     shapes the recommendation, not the reverse.
  7. CONSEQUENCES — name positive and negative consequences. Explicitly note whether a
     walking skeleton should be built before the full implementation begins (Rule B2),
     and why.
  8. OPERABILITY PLAN [GATE] — complete all required sub-fields: metrics, logs, traces,
     alerts, rollback plan, capacity headroom, known failure modes. If this section is
     absent or skeletal, the design doc is not ready for review.
  9. OPEN QUESTIONS — list unresolved questions with owners and resolution deadlines.
  10. REVIEW HAND-OFF — share the document for review before any implementation begins.
      Implementation begins only after the design doc is accepted.
artefact_template: |
  ---
  name: <design name>
  status: draft | in-review | accepted | superseded
  authors: <names>
  created: <YYYY-MM-DD>
  last_updated: <YYYY-MM-DD>
  supersedes: <path to prior doc, or "none">
  ---

  # <Design title>

  ## Problem
  <!-- What is wrong or missing? Who is affected, and how? What does current behaviour
       look like vs. desired behaviour? No solution language in this section. -->

  ## Context
  <!-- Background, history, related prior decisions (link ADRs). What has been tried
       before? What constraints exist that were inherited rather than chosen? -->

  ## Constraints
  <!-- Functional requirements (what the system must do) and non-functional requirements
       (how well it must do it). NFRs must have numbers: latency at p95, availability
       SLO, throughput, cost envelope. Each NFR names its fitness function — the
       automated check that will verify it continuously. -->

  ## Alternatives considered
  <!-- At least two alternatives, including "do nothing." For each: a brief description,
       the blast radius if this option turns out to be wrong, and the reversal cost.
       A section listing only the chosen approach is incomplete. -->

  ## Recommended approach
  <!-- The proposed solution. Why it wins on the named constraints. This section comes
       last because the problem shapes the recommendation. -->

  ## Consequences
  <!-- Positive and negative. Note explicitly whether a walking skeleton should precede
       the full build (and why), or whether the path is clear to proceed. -->

  ## Operability plan
  <!-- Metrics (what to graph), structured logs (what to emit), traces (spans to
       instrument), alerts (thresholds and on-call routing), rollback plan (steps and
       time estimate), capacity headroom, known failure modes with mitigations,
       upstream and downstream dependency failure modes. This section is required.
       Its absence is a reject condition. -->

  ## Open questions
  <!-- Unresolved questions. Each has an owner and a resolution deadline. -->
common_rationalisations: |
  | Rationalisation | Counter-argument |
  |---|---|
  | "It's too small to need a doc — we'll figure it out in the code." | Check Rule A1. If any trigger fires, the doc comes first; "figuring it out in the code" is exactly the build trap the trigger conditions were designed to catch. If no trigger fires, write a short ADR instead. |
  | "We already know what to build — the doc is just overhead." | The Alternatives and Constraints sections exist to surface what you don't know you don't know. A design doc with only the chosen solution is incomplete by Rule A2. If the outcome is truly obvious, the doc will be short and the overhead will be low. |
  | "We can write the doc after we understand the design better." | The design doc is how you understand the design better. Problem-first structure means the document shapes understanding; it is not a record of understanding already achieved. Post-hoc docs rationalise rather than evaluate. |
  | "The Operability section can be filled in closer to launch." | Rule A6 and Universal P6 are explicit: the operability plan exists before the build begins, and is authored with the people who will operate it — not delivered to them later. "Add it later" means it never gets the scrutiny it needs. |
  | "We don't have enough alternatives to fill that section." | The "do nothing" option is always an alternative. If you cannot describe what's wrong with the alternatives, you cannot explain why the recommended approach is right. A design doc that skips alternatives is not a design doc; it is an announcement. |
references: |
  - eng-principles-universal.md — P2, Rule A1, A2, A4, A5, A6, B2, B3
  - eng-principles-agentic.md — P1, P3
  - Larson, Will — "Staff Engineer" (trigger conditions for design docs)
  - Nygard, Michael — "Release It!" (operability; ADR format)
  - Cockburn, Alistair — walking skeleton (Rule B2 source)
  - Ford, Parsons, Kua — "Building Evolutionary Architectures" (fitness functions; Rule A5 source)
  - references/nfr-categories.md (NFR taxonomy for Rule A4)
dependencies:
  prerequisite_artefacts:
    - eng-principles-universal.md (must be accepted; provides Rules A1, A2, A4, A5, A6, B2, B3)
    - eng-principles-agentic.md (must be accepted; provides P1, P3)
  invokes:
    - incremental-implementation (hand-off after design doc is accepted)
  invoked_by:
    - idea-triage (may route to design-doc when a triaged idea clears the A1 threshold)
authoring_notes: |
  This is the first full skill in the engineering track. It sets the register for
  subsequent engineering skills — author should read idea-triage (accepted) for voice
  calibration before drafting.

  The skill must not produce implementation code. Its deliverable is the document.
  Any workflow step that drifts toward "and then implement X" is out of scope.

  The seven-section structure from Rule A2 is the non-negotiable spine. The artefact
  template above is what the skill produces; every section heading must appear in the
  output. Authors should not offer flexibility on section order or allow sections to be
  merged.

  The "Alternatives considered" section is where most reviewers and agents fall short.
  The skill must be explicit that listing only the chosen approach is an incomplete
  design doc — not a stylistic preference, a rule.

  Walking skeleton (Rule B2) is embedded in the Consequences section, not its own
  standalone step. The skill recommends it as the first build step in the hand-off to
  incremental-implementation, not as a sub-step within the design doc itself.

  Voice: direct and opinionated. No hedging. Short sentences where possible. No emoji.
  Sentence-case headings. Match the register of eng-principles-universal.md — the
  source principles documents are the calibration target, not addy's skill.

  Length target is 250–300 lines. The artefact template itself will consume roughly
  60–80 lines; the workflow, when, and rationalisations sections together will consume
  the bulk of the remainder. Watch for over-explanation in the workflow steps — each
  step should be executable without interpretation, not exhaustive.

  The `references/nfr-categories.md` file does not yet exist at brief time; it is a
  reference file that will be authored alongside this skill. Author should note this in
  the draft and leave the citation in place — the consistency checker will flag if it's
  missing at merge time.
