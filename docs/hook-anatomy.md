# Hook anatomy

The authoring spec for `HOOK.md` files in `hooks/<name>/`.

Hooks are mechanical checks that run on events (commit, PR, completion claim) to catch failure modes the agent has every reason not to flag against itself. They are not skills in disguise — fail criteria must be deterministic. If the check requires judgement, author a sub-agent persona instead.

## Frontmatter

```yaml
---
name: <hook-name>
description: <1-2 sentences>
category: hook
pack: <product | engineering | meta>
trigger_event: <commit | pr | completion-claim | merge>
principles_implemented:
  - source: <eng-universal | eng-agentic | roadmap | product>
    id: <principle or rule id>
    bucket: hook
length_target: <e.g. 60-100>
author: Anton Babushkin
predecessor:
  repo: <URL or "none">
  skill: <skill name in source repo, or "none">
  relation: <derivative | adjacent | new>
kept_from_predecessor: <list, or "n/a">
changed_from_predecessor: <list, or "n/a">
---
```

## Sections

In this exact order:

1. **Title** — `# <Hook Name>`
2. **Purpose** — one paragraph: what failure mode this hook catches and why a human or sub-agent can't catch it cheaply
3. **Trigger event** — exactly when this hook fires
4. **Check** — what it inspects, in language a regex / AST / linter could implement
5. **Fail criteria** — what triggers a fail; deterministic, no judgement words
6. **Pass criteria** — what allows the hook to pass; explicit so authors can't drift
7. **On fail** — what guidance the agent gets to fix
8. **Out of scope** — failure modes this hook does *not* catch (so other hooks know what to cover)
9. **References** — principles enforced

## Length

Target 60–100 lines. Hooks longer than 100 lines are usually skills in disguise. Editor pushes back on inflation.

## Reject triggers specific to hooks

- Fail criteria use words like "probably", "usually", "consider whether" — non-deterministic.
- The hook's check requires loading or interpreting prose. Hooks operate on structured signals: file paths, regex matches, AST patterns, line counts, file pairs.
- The hook duplicates a check another hook already performs.
- The hook asks the agent to make a judgement rather than measuring something.

## See also

- `docs/skill-anatomy.md`, `docs/sub-agent-anatomy.md`
- `docs/brief-template.md`
- `docs/authoring-learnings.md`
