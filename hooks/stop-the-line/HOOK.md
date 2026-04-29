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

Agents are optimised to make errors disappear. Silencing a failing signal — suppressing the type system, adding a compiler override, skipping a test, suppressing a static analysis warning, deleting an assertion — achieves that faster than investigating the root cause. The failure mode is consistent and predictable: it appears in every training corpus, and agents reach for it under pressure without a hard constraint. A human reviewer can catch obvious suppressions in a focused review, but cannot catch them reliably at scale across many small PRs. Principle 6 names the rule; this hook enforces it mechanically at the PR level, reading only the diff so it flags new suppressions in the current change, not pre-existing ones.

## Trigger event

Fires on PR open and PR update. Input is the PR diff: added lines (`+` lines), file paths, and test-file line counts before and after. The hook is non-blocking by design: it surfaces findings and returns the work for investigation; it does not veto the PR automatically.

## Check

Scans added lines only, not the full file. Five categories:

1. Added lines matching `<type-suppress-pattern>` (e.g. unsafe cast to a top type, forced type override), outside of comments and string literals. The pattern can appear legitimately in doc strings and inline comments — those are excluded.
2. Added lines matching `<compiler-suppress-pattern>` (e.g. inline directives that tell the compiler to ignore an error on the next line or block).
3. Added lines matching `<test-skip-pattern>` in test files (e.g. markers that exclude a test from the run). Test-file detection uses file path conventions (`*_test.*`, `*.spec.*`, `tests/`, or equivalent).
4. Added lines matching `<lint-suppress-pattern>` (e.g. inline comments or annotations that silence a static analyser warning).
5. Test-file line count in this PR is lower than in the base branch, while non-test changed files also exist in the PR. This check is line-count comparison, not regex. It is advisory: assertion deletions carry the highest false-positive rate (comments removed, imports consolidated). List the finding; the agent weighs context.

## Fail criteria

Any one of the following in the diff is a fail. Multiple findings are all reported.

- `<type-suppress-pattern>` appears in added lines outside comments and string literals.
- `<compiler-suppress-pattern>` appears in added lines.
- `<test-skip-pattern>` appears in added lines in test files.
- `<lint-suppress-pattern>` appears in added lines.
- A test file's line count is lower in this PR than in the base branch while non-test changed files also exist in the PR. (Advisory.)

## Pass criteria

No added line matches any fail criterion. Test file line counts are unchanged or higher.

## On fail

List each finding: pattern matched, file, line number. For assertion-deletion findings: file, line count before, line count after.

The work is returned for investigation. Investigate the flagged signal. Not "consider investigating" — investigate. If the suppression silences a genuine failure, fix the root cause. If it silences a false positive from the tool, configure the tool to exclude that case at the project level; do not suppress inline. If the deleted test was wrong, document why and what replaces it. Merging the suppression is not an option.

Reference: Agentic Principle 6 — stop the line on first failure; never silence the signal.

## Out of scope

- PR size (line count) and branch age — covered by `small-batch` (Next).
- Completion-claim evidence — covered by `evidence-claim` (Next).
- Pre-existing suppressions not touched by this PR's diff.
- Whether the suppressed signal was correct — that is a sub-agent judgement call, not a mechanical check.

## References

- Eng Agentic Principle 6: Stop the line on first failure; never silence the signal
- Eng Universal Rule C4: CI stays green; a red build is the team's top priority
