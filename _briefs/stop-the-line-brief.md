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
    note: Mechanically catches the suppression moves agents make instead of investigating failures — any-cast, ts-ignore, skip, eslint-disable, deleted assertions
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
  Agents are optimised to make errors disappear. Silencing a failing signal — casting to `any`,
  adding `@ts-ignore`, skipping a test, suppressing a lint warning, deleting an assertion —
  achieves that goal faster than investigating the root cause. This hook catches those moves at
  the PR level, before they merge. It reads the diff, not the full codebase, so it flags only
  new suppressions introduced by the current change, not pre-existing ones. When it fires, the
  work goes back for investigation — not for re-suppression. The check is deterministic: each
  pattern either appears in the diff or it does not. No judgement is required of the agent running
  the hook. This is the pack's first hook, establishing the failure-mode-detection pattern that
  `small-batch` and `evidence-claim` will follow.
scope:
  in: |
    Four pattern categories, stack-agnostic. Each category has a named example; the hook body
    supplies `<suppress-pattern>` placeholders for stack-specific implementations.

    - Type suppressions added in the diff: unsafe casts that silence the type system
      (e.g. `as any` / `: any` in TypeScript; `# type: ignore` in Python; `@SuppressWarnings` in Java)
    - Compiler/analyser directives that suppress errors added in the diff
      (e.g. `// @ts-ignore`, `// @ts-nocheck` in TypeScript; `//nolint` in Go; `[SuppressMessage]` in C#)
    - Test-skip markers added in test files in the diff
      (e.g. `.skip(` in Jest/Mocha/Vitest; `@pytest.mark.skip` in Python; `t.Skip()` in Go)
    - Static analysis suppressions added in the diff
      (e.g. `eslint-disable` in JS/TS; `# noqa` in Python; `#[allow(...)]` in Rust)
    - Assertion deletions: test file line count drops while non-test code changes exist in the same PR
      (language-agnostic; line-count comparison)
  out: |
    - PR size (line count, branch age) — covered by `small-batch` (Next)
    - Completion-claim evidence — covered by `evidence-claim` (Next)
    - Pre-existing suppressions in the codebase — this hook flags new additions in the diff only
    - Whether the suppressed signal was correct (i.e. was the skipped test testing the right thing) — that is a sub-agent judgement call, not a mechanical check
    - Test-isolation markers (e.g. `.only(`) — these silence other tests rather than suppress a signal; author decides whether to include in scope or keep as advisory note
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
  2. SCAN added lines for suppression patterns (stack-agnostic categories; examples in parens):
     - Gate A: type suppression added (`as any` in TS; `# type: ignore` in Python; `@SuppressWarnings` in Java; `<suppress-type-pattern>`) → FAIL with pattern, file, line
     - Gate B: compiler/analyser directive suppression added (`@ts-ignore`/`@ts-nocheck` in TS; `//nolint` in Go; `<suppress-analyser-pattern>`) → FAIL with pattern, file, line
     - Gate C: test-skip marker added in test file (`.skip(` in Jest/Vitest; `@pytest.mark.skip`; `t.Skip()`; `<skip-pattern>`) → FAIL with pattern, file, line
     - Gate D: static analysis suppression added (`eslint-disable` in JS/TS; `# noqa`; `#[allow(...)]`; `<lint-suppress-pattern>`) → FAIL with pattern, file, line
     - Gate E: test file line count drops while non-test changed files exist → FAIL with file, before/after count
  3. COLLECT all findings across all gates
  4. REPORT findings — if any gate fired: list each finding (pattern, file, line); state that the work is returned for investigation, not re-suppression; do not block the PR automatically
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

  [What the hook scans — added lines only, not the full file. Patterns listed precisely,
  with placeholder commands for stack-specific implementations. Test-file detection note.
  Assertion-deletion check described separately (line-count comparison, not regex).]

  ## Fail criteria

  [One criterion per suppression type. No judgement words. Each criterion is binary:
  the pattern appears in the diff, or it does not.]

  One criterion per pattern category. Each is binary — pattern present in diff or not.

  - A type suppression (`<type-suppress-pattern>`, e.g. `as any` in TS) appears in
    added lines outside comments and string literals.
  - A compiler/analyser directive suppression (`<analyser-suppress-pattern>`, e.g.
    `@ts-ignore` in TS) appears in added lines.
  - A test-skip marker (`<skip-pattern>`, e.g. `.skip(` in Jest) appears in added lines
    in test files.
  - A static analysis suppression (`<lint-suppress-pattern>`, e.g. `eslint-disable` in
    JS/TS) appears in added lines.
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

  "The eslint rule is wrong for this case."
  Counter: if the rule is wrong for a case, configure the rule to exclude that case in the project
  configuration — don't suppress it inline. Inline suppression hides the exception from the rule's
  scope and makes future audits impossible.

  "The test I deleted was testing the wrong thing."
  Counter: this is exactly the judgement call the hook is designed to surface. If the test was wrong,
  document why it was wrong and what replaces it. A deletion without documentation is indistinguishable
  from a deletion to silence a failure.

  "This is a small PR; the pattern isn't a real risk here."
  Counter: the hook has no size floor by design. Small PRs can carry the same failure modes as large
  ones. The cost of investigation is low; the cost of a suppression that ships is not.
references: |
  - skills/engineering/eng-principles-agentic.md — Principle 6 (primary source; the implication
    paragraph names this hook by name)
  - skills/engineering/eng-principles-universal.md — Rule C4 (CI stays green; adjacent)
  - skills/engineering/eng-principles-universal.md — Principle 8 (small batches; adjacent, referenced
    in Out of scope boundary with small-batch hook)
  - docs/hook-anatomy.md — authoring spec for HOOK.md files
  - docs/brief-template.md — this brief's format
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

  2. Type-suppression detection has a known false-positive risk: the pattern string can appear in
     comments, strings, and docs. The criterion must specify "outside of comments and string
     literals." The author uses `<type-suppress-pattern>` as the placeholder and notes the
     false-positive risk — the hook does not hard-code any language's specific syntax.

  3. `.only(` detection applies to Jest, Mocha, Vitest, and similar frameworks. The hook does not
     need to enumerate frameworks — `.only(` is the pattern; it fires regardless of which framework
     uses it.

  4. The assertion-deletion check (line count) is the least precise of the six criteria and carries
     the highest false-positive risk (comments removed, imports consolidated, etc.). The author should
     flag this in the hook body and note that this criterion is advisory: findings should be listed
     but the agent is told to weigh the context. This is the one criterion that approaches the
     judgement boundary — keep the language cautious.

  5. The hook is non-blocking. This is a design decision, not a concession. The implication of
     Agentic P6 is that the work goes back for investigation; automatic PR veto is not in scope for
     v0.1 (that would require runtime integration, which is a v0.2 non-goal per PROJECT_PLAN.md §2).
     The hook ships as a spec; integration is deferred.

  6. Do not add a "severity" or "warning vs. error" distinction. All six criteria are the same
     severity — each one signals a potential silenced failure. Tiering introduces the rationalisation
     "this is only a warning" and weakens the rule.

  7. The voice in the "On fail" section should match the directness of Principle 6 itself. Avoid
     softening language ("consider investigating", "you may want to check"). The instruction is:
     investigate the flagged signal. Full stop.

  8. Line target is 60–100. The hook anatomy is dense by design — Purpose, Trigger, Check, Fail
     criteria, Pass criteria, On fail, Out of scope, References. The content above maps cleanly to
     that structure. If the draft exceeds 100 lines, the author has inflated either the Check section
     (too much implementation detail — use placeholders) or the On fail section (too much prose —
     cut to instructions). Editor will push back.
