PR-level hook that scans incoming diffs for signal-suppression moves: type suppressions, compiler directives, test skips, static-analysis suppressions, and deleted assertions. Fires on every PR with a diff — no size floor. Uses five pattern categories expressed as stack-agnostic placeholders; the hook body gives per-stack examples for illustration only. Non-blocking by design: when it fires, the work goes back for investigation, not re-suppression. Establishes the failure-mode-detection pattern that `small-batch` and `evidence-claim` (both Next) will follow.

---

artefact: stop-the-line
category: hook
pack: engineering
roadmap_position: now
lifecycle_stage: build/verify
length_target: 60–100 lines
predecessor:
  repo: none
  skill: none
  relation: new
  url: none
prior_art_notes:
  read_first: n/a
  keep: n/a
  change: n/a
  do_not_copy: n/a
principles_implemented:
  - source: eng-agentic
    id: P6
    bucket: hook
    note: Mechanically catches the four suppression moves agents make instead of investigating failures — type casts, compiler directives, test skips, static-analysis suppressions, deleted assertions
  - source: eng-universal
    id: P8
    bucket: embedded
    note: Adjacent — large PRs make suppression harder to spot; referenced in Out of scope, not checked here
  - source: eng-universal
    id: C4
    bucket: embedded
    note: Adjacent — CI staying green is the goal; silencing signals is the failure mode this hook guards against
triage_record_ref: "PROJECT_PLAN.md §11.1 row #7 — confidence 6; evidence: felt-pain evidence (any-cast, .skip, lint suppression); deterministic checks"
purpose: >
  Agents are optimised to make errors disappear. Silencing a failing signal — suppressing
  the type system, adding a compiler override, skipping a test, suppressing a static analysis
  warning, deleting an assertion — achieves that goal faster than investigating the root cause.
  This hook catches those moves at the PR level, before they merge. It reads the diff, not
  the full codebase, so it flags only new suppressions introduced by the current change, not
  pre-existing ones. When it fires, the work goes back for investigation — not for
  re-suppression. The check is deterministic: each pattern either appears in the diff or it
  does not. No judgement is required of the agent running the hook. This is the pack's first
  hook, establishing the failure-mode-detection pattern that `small-batch` and `evidence-claim`
  will follow.
scope:
  in: |
    Five pattern categories, expressed as placeholders. The hook body gives one or two
    per-stack examples for illustration only — the criteria themselves are stack-agnostic.

    - Type suppressions added in the diff: `<type-suppress-pattern>` — unsafe casts that
      silence the type checker
    - Compiler/analyser directives that suppress errors added in the diff:
      `<compiler-suppress-pattern>` — inline comments or annotations that tell the compiler
      to ignore an error on the next line or block
    - Test-skip markers added in test files in the diff: `<test-skip-pattern>` — markers
      that cause a test to be excluded from the run
    - Static analysis suppressions added in the diff: `<lint-suppress-pattern>` — inline
      comments or annotations that silence a linter or static analyser warning
    - Assertion deletions: test file line count drops while non-test code changes exist in
      the same PR (language-agnostic; line-count comparison)
  out: |
    - PR size (line count, branch age) — covered by `small-batch` (Next)
    - Completion-claim evidence — covered by `evidence-claim` (Next)
    - Pre-existing suppressions in the codebase — this hook flags new additions in the diff only
    - Whether the suppressed signal was correct (i.e. was the skipped test testing the right
      thing) — that is a sub-agent judgement call, not a mechanical check
    - Test-isolation markers (`<test-only-pattern>`) — these silence other tests rather than
      suppress a failing signal; author decides whether to include as a sixth criterion or note
      as advisory
size_triggers:
  fires_for: "Any PR that includes a diff — there is no size floor. A one-line change that adds a suppression pattern fires the hook."
  does_not_fire_for: "PRs with no diff (empty commits, tag-only changes). Pre-existing suppressions not touched by the diff do not re-trigger the hook."
inputs: |
  The PR diff. Specifically:
  - Added lines (`+` lines) across all changed files
  - File paths for changed files, to distinguish test files from non-test files
  - Line counts for test files before and after the change (for assertion-deletion detection)
  The hook does not require a running environment, compiled output, or any external service call.
outputs:
  artefact_path: hooks/stop-the-line/HOOK.md
  artefact_name: HOOK.md
workflow_outline: |
  1. RECEIVE diff — the hook is triggered on PR open or update; input is the PR diff
  2. SCAN added lines for suppression patterns:
     - Gate A: `<type-suppress-pattern>` in added lines outside comments and string literals → FAIL with pattern, file, line
     - Gate B: `<compiler-suppress-pattern>` in added lines → FAIL with pattern, file, line
     - Gate C: `<test-skip-pattern>` in added lines in test files → FAIL with pattern, file, line
     - Gate D: `<lint-suppress-pattern>` in added lines → FAIL with pattern, file, line
     - Gate E: test file line count drops while non-test changed files exist → FAIL with file, before/after count
  3. COLLECT all findings across all gates
  4. REPORT findings — if any gate fired: list each finding (pattern, file, line); state that
     the work is returned for investigation, not re-suppression; do not block the PR automatically
  5. PASS — if no gate fired, report clean and allow the PR to proceed

  The hook is non-blocking by design. It surfaces findings and returns the work; it does not veto the PR.
  The agent receiving the findings must investigate the flagged signal, not rephrase the suppression.
artefact_template: |
  ```markdown
  ---
  name: stop-the-line
  description: >
    Catches signal-suppression moves in PR diffs — type suppressions, compiler directives,
    test skips, static-analysis suppressions, deleted assertions. Stack-agnostic; examples
    given for common stacks. Returns the work for investigation, not re-suppression.
    Traces to Eng Agentic Principle 6.
  category: hook
  pack: engineering
  trigger_event: pr
  principles_implemented:
    - source: eng-agentic
      id: P6
      bucket: hook
    - source: eng-universal
      id: C4
      bucket: embedded
  length_target: 60–100
  author: Anton Babushkin
  predecessor:
    repo: none
    skill: none
    relation: new
  kept_from_predecessor: n/a
  changed_from_predecessor: n/a
  ---

  # Stop the line

  ## Purpose

  [One paragraph: the failure mode (agents silence signals rather than investigate);
  why it's consistent and predictable; why a human or sub-agent can't catch it cheaply at scale;
  why this hook exists alongside Principle 6 rather than relying on Principle 6 alone.]

  ## Trigger event

  Fires on PR open and PR update. Input is the PR diff.

  ## Check

  [What the hook scans — added lines only, not the full file. Patterns expressed as
  `<placeholder>` with per-stack examples in parentheses for illustration.
  Test-file detection note. Assertion-deletion check described separately (line-count
  comparison, not regex).]

  ## Fail criteria

  One criterion per pattern category. Each is binary — pattern present in diff or not.

  - `<type-suppress-pattern>` appears in added lines outside comments and string literals.
  - `<compiler-suppress-pattern>` appears in added lines.
  - `<test-skip-pattern>` appears in added lines in test files.
  - `<lint-suppress-pattern>` appears in added lines.
  - A test file's line count is lower in this PR than in the base branch while non-test
    changed files also exist in the PR.

  Any one criterion firing is a fail. Multiple findings are all reported.

  ## Pass criteria

  No added line matches any fail criterion. Test file line counts are unchanged or higher.

  ## On fail

  [What the agent is told: findings listed by file and line; the instruction to investigate
  the flagged signal rather than rephrase the suppression; reference to Agentic P6 and the
  implication that the hook returning work is the expected outcome, not an indictment.]

  ## Out of scope

  [PR size and branch age — `small-batch` (Next). Completion-claim evidence — `evidence-claim`
  (Next). Pre-existing suppressions not touched by this PR's diff. Correctness of the suppressed
  signal itself — that requires sub-agent judgement.]

  ## References

  - Eng Agentic Principle 6: Stop the line on first failure; never silence the signal
  - Eng Universal Rule C4: CI stays green; a red build is the team's top priority
  ```
common_rationalisations: |
  "The suppression is temporary — I'll fix it later."
  Counter: temporary suppressions become permanent. The hook fires on every PR, not just the
  ones where you intend to leave it. Fix the root cause now or open a tracked follow-up before
  merging; do not merge the suppression.

  "I skipped the test because it was flaky, not because it was wrong."
  Counter: flaky tests are bugs (Eng Universal Rule C4). A flaky test belongs in a fix-or-delete
  decision with a tracked issue, not silently skipped. The hook fires regardless — investigate and
  decide explicitly.

  "The static analysis rule is wrong for this case."
  Counter: if the rule is wrong for a case, configure the rule to exclude that case at the project
  level — don't suppress it inline. Inline suppression hides the exception from the rule's scope
  and makes future audits impossible.

  "The test I deleted was testing the wrong thing."
  Counter: this is exactly the judgement call the hook is designed to surface. If the test was
  wrong, document why it was wrong and what replaces it. A deletion without documentation is
  indistinguishable from a deletion to silence a failure.

  "This is a small PR; the pattern isn't a real risk here."
  Counter: the hook has no size floor by design. Small PRs can carry the same failure modes as
  large ones. The cost of investigation is low; the cost of a suppression that ships is not.
references: |
  - skills/engineering/eng-principles-agentic.md — Principle 6 (primary source; the implication
    paragraph names this hook by name)
  - skills/engineering/eng-principles-universal.md — Rule C4 (CI stays green; adjacent)
  - skills/engineering/eng-principles-universal.md — Principle 8 (small batches; adjacent, referenced
    in Out of scope boundary with small-batch hook)
  - docs/hook-anatomy.md — authoring spec for HOOK.md files
dependencies:
  prerequisite_artefacts: |
    - skills/engineering/eng-principles-agentic.md — must be at draft stage before this hook is
      authored (see PROJECT_PLAN.md §8.1: hook track gated on agentic principles draft)
  invokes: none
  invoked_by: |
    - Any PR-level automation or agent review that runs the hook pack
    - Referenced by eng-principles-agentic.md P6 implication paragraph
authoring_notes: |
  1. The fail criteria section is the hardest part to get right. Each criterion must be expressible
     as a regex, AST pattern, or line-count comparison. If any criterion requires prose interpretation,
     move it out of scope or author a sub-agent instead.

  2. The hook is stack-agnostic. Express all fail criteria using `<placeholder>` syntax. In the
     Check section, give one or two per-stack examples in parentheses — enough to make the category
     concrete — but the criteria themselves never name a specific language or tool. The author's
     job is to describe the pattern category, not to enumerate every stack's variant.

  3. Type-suppression detection has a known false-positive risk: the pattern string can appear in
     comments, strings, and docs. The criterion must specify "outside of comments and string
     literals." Note this in the Check section; it applies regardless of which stack's syntax
     the implementer uses.

  4. The assertion-deletion check (line count) is the least precise criterion and carries the
     highest false-positive risk (comments removed, imports consolidated, etc.). Flag this in
     the hook body and label the criterion advisory: findings should be listed but the agent is
     told to weigh the context. This is the one criterion that approaches the judgement boundary.

  5. The hook is non-blocking. This is a design decision, not a concession. The implication of
     Agentic P6 is that the work goes back for investigation; automatic PR veto is not in scope
     for v0.1 (runtime integration is a v0.2 non-goal per PROJECT_PLAN.md §2). The hook ships
     as a spec; integration is deferred.

  6. Do not add a "severity" or "warning vs. error" distinction. All criteria are the same
     severity — each signals a potential silenced failure. Tiering introduces the rationalisation
     "this is only a warning" and weakens the rule.

  7. The voice in the "On fail" section must match the directness of Principle 6. No softening:
     not "consider investigating," not "you may want to check." The instruction is: investigate
     the flagged signal. Full stop.

  8. Line target is 60–100. If the draft exceeds 100 lines, the Check section has too much
     implementation detail (use placeholders) or the On fail section has too much prose (cut to
     instructions). Editor will push back.
