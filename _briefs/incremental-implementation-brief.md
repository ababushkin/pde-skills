Takes an accepted design doc and implements it in thin vertical slices, walking skeleton first. This is the operational form of Rule B2 and Principle 8 — the skill enforces small-batch discipline structurally, making it impossible to complete without a working end-to-end path before feature logic begins. Each slice has a mandatory test-then-implement-then-verify loop; the skill stops at any failing build rather than continuing. Hands off from design-doc and hands off to deploy (Next) once implementation is complete. Does not produce a standalone artefact — the output is code and commits. Two scope decisions to note: (1) the walking skeleton gate has an escape hatch for trivially small implementations with no integration surface (judgment call, named explicitly in the skill); (2) KTLO bug fixes are covered by this skill's per-slice TDD loop — write a failing test that reproduces the bug, fix it, verify green — without the design-doc requirement or walking skeleton gate. This makes the skill the single place for all implementation work, not just design-doc-backed features.

---

```yaml
artefact: incremental-implementation
category: skill
pack: engineering
roadmap_position: now
lifecycle_stage: build
length_target: 200–250 lines
predecessor:
  repo: https://github.com/addyosmani/agent-skills
  skill: incremental-implementation
  relation: derivative
  url: https://github.com/addyosmani/agent-skills/blob/main/skills/incremental-implementation/SKILL.md
prior_art_notes:
  read_first:
    - skills/engineering/eng-principles-universal.md (P4, P5, P8, Rules B1, B2, B3, C1, C4, C8)
    - skills/engineering/eng-principles-agentic.md (P1, P3, P6)
    - addy's incremental-implementation skill (predecessor)
    - skills/engineering/design-doc/SKILL.md (feeds into this skill)
  keep: >
    Slice-by-slice delivery discipline. The instinct that each increment should
    be independently verifiable. Test-implement-verify as the per-slice unit of work.
  change: >
    1. Walking skeleton is a mandatory first gate, not an optional recommendation.
       Pre-skeleton work is not permitted — the gate is hard.
    2. Stop-the-line integration: a failing build or failing test is a stop signal,
       not a continuable state. Agents proceeding past a failing build is the specific
       failure mode this skill guards against (Agentic P6; stop-the-line hook invoked).
    3. Design doc is a required input, not an optional one. The spec holds the work
       (Agentic P3); drift from the accepted design doc is an explicit failure mode.
    4. Per-slice open question surfacing is a named step: if a slice surfaces a new
       open question or invalidates a design assumption, the slice stops and the question
       goes back to the design doc before the slice continues.
    5. YAGNI enforcement per slice: Rule B1 applies within each slice — implement the
       smallest thing that satisfies the slice's acceptance criterion.
  do_not_copy: >
    No paragraph from addy's skill is reproduced verbatim. Author reads it as input
    and authors fresh.
principles_implemented:
  - source: eng-universal
    id: P4
    bucket: embedded
    note: Walking skeleton gate is the operational form of "test risky assumptions first"; pre-skeleton estimates are named as uncalibrated.
  - source: eng-universal
    id: P5
    bucket: embedded
    note: Rule B1 (YAGNI) applied per slice — minimum code to satisfy the slice's acceptance criterion; speculative flexibility is out of scope.
  - source: eng-universal
    id: P8
    bucket: standalone
    note: The entire skill is the operational form of small-batch discipline — walking skeleton, thin slices, per-slice verification, short-lived commits.
  - source: eng-universal
    id: Rule B1
    bucket: embedded
    note: Per-slice YAGNI gate; the skill instructs the implementer to write the minimum code that satisfies the slice's test, not the most general solution.
  - source: eng-universal
    id: Rule B2
    bucket: standalone
    note: Walking skeleton is the first step and a hard gate — no feature slices begin until the skeleton is complete and deploying.
  - source: eng-universal
    id: Rule B3
    bucket: embedded
    note: When a slice surfaces a new approach decision, blast radius and reversibility must be named before the decision is taken.
  - source: eng-universal
    id: Rule C1
    bucket: embedded
    note: Short-lived branches per slice; trunk-based development as the default commit pattern.
  - source: eng-universal
    id: Rule C4
    bucket: embedded
    note: CI must stay green throughout; a failing build stops slice work (this is the universal rule that Agentic P6 amplifies for agent contexts).
  - source: eng-universal
    id: Rule C8
    bucket: embedded
    note: Tests are specification of slice behaviour; written before or alongside the implementation, not after.
  - source: eng-agentic
    id: P1
    bucket: embedded
    note: Skill requires loading design doc, ADRs, and relevant principles before starting — context is the asset.
  - source: eng-agentic
    id: P3
    bucket: embedded
    note: Design doc is the spec that holds the work; drift from the accepted doc is an explicit failure mode requiring explicit re-scoping.
  - source: eng-agentic
    id: P6
    bucket: embedded
    note: Failing build or failing test triggers stop-the-line; agent must investigate root cause before continuing any slice work. Invokes stop-the-line hook.
triage_record_ref: "PROJECT_PLAN.md §11.1, row #6 — confidence 6, evidence: personal usage of addy's version; most-fired skill"
purpose: >
  incremental-implementation takes an accepted design doc and builds it in thin
  vertical slices, starting with a walking skeleton. It is the operational form of
  Rule B2 (walking skeleton first) and Principle 8 (small batches beat big batches):
  the skill enforces small-batch discipline structurally by making a working end-to-end
  path the precondition for any feature logic, and by requiring each slice to be tested
  and verified before the next begins. The spec (the accepted design doc) holds the work
  throughout — drift from the accepted doc is an explicit failure mode, not a stylistic
  concern. When a failing build or test appears, work stops; the stop-the-line hook is
  the mechanical enforcement of this at the PR level.
scope:
  in: >
    Walking skeleton: minimal end-to-end path through every real component. Slicing the
    design doc into thin vertical increments. Per-slice test-implement-verify loop.
    Open question surfacing when a slice invalidates a design assumption. YAGNI discipline
    per slice (Rule B1). Stop-the-line discipline when a build fails (Agentic P6).
    Staying within the accepted design doc's scope; explicit re-scoping when that boundary
    needs to move.
  out: >
    Writing or revising the design doc — that is design-doc skill. Deployment to production
    — that is deploy (Next). Post-launch review — that is post-launch-impact-review (Next).
    Test strategy design at the project level — this skill writes per-slice tests; it does
    not design the overall test strategy. Planning and task breakdown at the project level
    — that is planning-and-task-breakdown (Next). KTLO bug fixes that don't have a design
    doc (Rule A5 carve-out; proceed directly to implementation).
size_triggers:
  fires_for: >
    Any implementation work that has an accepted design doc. The skill applies regardless
    of the size of the implementation — the walking skeleton discipline and per-slice
    verification are not optional for large projects only.
  does_not_fire_for: >
    Exploratory work without an accepted design doc — run a spike or write a design doc
    first. Work that is already in progress without a walking skeleton — this skill does
    not backfill; it governs from the start. Note: KTLO bug fixes DO use this skill's
    per-slice TDD loop (see Bug fix sub-workflow in workflow_outline) but skip the design
    doc requirement and walking skeleton gate.
inputs: >
  An accepted design doc at docs/design-docs/<name>/design-doc.md. Relevant ADRs.
  Access to eng-principles-universal.md (Rules B1, B2, B3, C1, C4, C8) and
  eng-principles-agentic.md (P1, P3, P6). A working build environment.
outputs:
  artefact_path: "code in the relevant source tree"
  artefact_name: "commits — one per verified slice, one for the walking skeleton"
workflow_outline: |
  1. CONTEXT LOAD [GATE] — load the accepted design doc, relevant ADRs, and principles.
     Name each artefact loaded. If no accepted design doc exists, stop — run design-doc
     first. Do not begin implementation against a draft or in-review doc.
  2. WALKING SKELETON [GATE] — implement the minimal end-to-end path: one request wired
     through every real component in the real deployment environment. No feature logic yet.
     The skeleton is done when it deploys and the key path works end-to-end. Commit it.
     Any estimate made before this point is uncalibrated; revise after the skeleton is in.
     Escape hatch: if the implementation is a single function or method with no integration
     surface (touches no external system, no deployment, no shared interface), the skeleton
     may be degenerate — the function itself is the skeleton. State this explicitly rather
     than silently skipping. The judgment call is: would a failing integration surprise
     wreck this work? If no, the gate is trivially satisfied. If yes, build the skeleton.
  3. SLICE IDENTIFICATION — break remaining design doc scope into thin vertical slices.
     Each slice must deliver observable behaviour; horizontal layers (e.g. "add all the
     database models") are not slices. Write the slice list; it becomes the per-slice
     checklist.
  4. PER-SLICE LOOP (repeat for each slice):
     a. Write the test(s) that specify this slice's acceptance criterion. Tests first.
     b. Implement the minimum code that makes those tests pass (Rule B1).
     c. [GATE] Verify: tests green, CI green. If any test or build fails, stop.
        Investigate the root cause (Agentic P6). Do not continue to the next step while
        CI is red.
     d. Commit the slice.
     e. Surface any open questions raised by this slice. If the slice invalidates a design
        assumption, pause, document the question, and resolve it before continuing.
  5. COMPLETION CHECK — verify all design doc requirements are covered, open questions are
     resolved or explicitly deferred, and fitness functions named in the design doc are
     passing. Flag any delta between the accepted design and what was built.

  BUG FIX SUB-WORKFLOW (KTLO; no design doc required):
  1. Write a failing test that reproduces the bug. The test is the spec.
  2. Fix the minimum code required to make the test pass (Rule B1).
  3. [GATE] Verify: test green, CI green. If other tests broke, investigate before continuing.
  4. Commit.
  No walking skeleton gate. No design doc. No slice list. The TDD loop is the entire workflow.
artefact_template: |
  Not applicable. The skill's output is code and commits.
  Optional: at step 3, the implementer may record the slice list as a checklist at the
  top of the relevant design doc's open questions section or in a working notes file.
  This is not required but aids tracking on multi-day implementations.
common_rationalisations: |
  | Rationalisation | Rebuttal |
  |---|---|
  | "We'll do the walking skeleton after we understand the codebase better." | Rule B2: pre-skeleton estimates are uncalibrated. The skeleton is exactly how you understand the codebase — it flushes out the integration surprises that wreck schedules. |
  | "This slice is too big to split." | If you can't split it, it's not a vertical slice — it's a horizontal layer. Break the feature into observable states: what can the user or system do after each step that it couldn't do before? |
  | "I'll write the tests after I understand the code better." | Rule C8: tests are specification, not coverage. Writing them first forces you to define the acceptance criterion before implementing it. "After" means after the decisions are already made — tests written then describe what you built, not what you meant to build. |
  | "The CI is failing but it's just a flaky test — I'll keep going." | Rule C4 and Agentic P6: flaky tests are bugs, and a failing build is a stop signal. Proceeding past a failing build is the specific failure mode the stop-the-line hook guards against. Fix the flaky test first. |
  | "The design doc changed while I was implementing — I'll just go with what I have." | Agentic P3: the spec holds the work. If the design doc changes, surface the delta explicitly, document it, and get it accepted. Don't silently build something different from the accepted doc. |
references: |
  - skills/engineering/eng-principles-universal.md — P4, P5, P8, Rule B1, B2, B3, C1, C4, C8
  - skills/engineering/eng-principles-agentic.md — P1, P3, P6
  - hooks/stop-the-line/HOOK.md — invoked when Agentic P6 fires (failing build in a slice)
  - skills/engineering/design-doc/SKILL.md — feeds into this skill as required input
  - Cockburn, Alistair — walking skeleton (Rule B2 source)
  - Humble & Farley — "Continuous Delivery" (small batches, trunk-based development)
  - Don Reinertsen — "Principles of Product Development Flow" (P8 source)
  - Beck, Kent — "Tidy First" (P5 source; YAGNI via XP)
dependencies:
  prerequisite_artefacts:
    - skills/engineering/design-doc/SKILL.md (required input is an accepted design doc)
    - skills/engineering/eng-principles-universal.md (must be accepted)
    - skills/engineering/eng-principles-agentic.md (must be accepted)
    - hooks/stop-the-line/HOOK.md (invoked by Agentic P6 implication)
  invokes:
    - hooks/stop-the-line/HOOK.md (when a failing build fires Agentic P6)
  invoked_by:
    - design-doc (hand-off once doc is accepted)
authoring_notes: |
  - The walking skeleton gate is the most important thing in this skill. It must be written
    as an unconditional first step — not "consider building a skeleton" but "build the
    skeleton; no feature slices begin until it deploys." If the draft softens this, the
    editor pushes back.
  - The stop-the-line integration is the key thing this skill adds over addy's version.
    Step 4c gate must name the stop signal explicitly and cross-reference Agentic P6 and
    the stop-the-line hook. "CI must stay green" is the rule; "stop and investigate" is
    the instruction; "not 'investigate later'" is the emphasis.
  - Agentic P3 (spec holds the work) is the guard against scope creep during implementation.
    The skill must say: if you find yourself building something not in the accepted design
    doc, stop and surface it — don't just build it and reconcile later.
  - The artefact template is not a file — the skill's output is commits. Author should make
    this clear and not invent a reporting artefact that adds process overhead. The optional
    slice checklist is optional; do not make it required.
  - Voice: match eng-principles-universal register — direct, no hedging. Gates are hard stops.
    "Verify" means "tests green AND CI green," not "check that it looks right."
  - Length target 200–250 lines. The common rationalisations table will consume ~20 lines.
    Workflow steps should be the densest section. Don't pad.
  - KTLO bug fixes are NOT exempt from this skill — they use the bug fix sub-workflow
    (failing test → fix → green). The carve-out is from the design doc requirement and
    walking skeleton gate, not from the skill entirely. Make this distinction clear.
  - The walking skeleton escape hatch must be written as a judgment call with a named
    criterion ("would a failing integration surprise wreck this work?"), not as a blanket
    exemption. The default is: build the skeleton.
```
