# Skill anatomy

The authoring spec for `SKILL.md` files in `skills/<name>/`.

## Frontmatter

```yaml
---
name: <skill-name>
description: <1-2 sentences, includes trigger phrases>
pack: <product | engineering | meta>
lifecycle_stage: <define | plan | build | ship | verify | review | meta | reference>
principles_implemented:
  - source: <eng-universal | eng-agentic | roadmap | product>
    id: <principle or rule id>
    bucket: <embedded | standalone | hook | sub-agent>
length_target: <e.g. 200-280>
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

1. **Title** — `# <Skill Name>`
2. **Purpose** — one paragraph
3. **When to use** — explicit trigger phrases and intents, with the size-the-work rubric where relevant
4. **When not to use** — explicit non-triggers, with the right alternative skill named
5. **Inputs** — what the skill expects to be given
6. **Outputs** — what it produces, including the artefact path under `docs/`
7. **Workflow** — numbered steps with hard gates marked `[GATE]`
8. **Artefact template** — the markdown the skill produces
9. **Common rationalisations** — table of typical excuses and rebuttals
10. **Red flags** — bullet list of signs the skill is being violated
11. **Verification / exit criteria** — how to know the skill ran correctly
12. **References** — pointers to `references/` and to source principles

## Length

Target 100–300 lines. Below 100, editor checks for under-specification (acceptable if genuinely complete). Above 300, editor checks for redundancy with other skills, scope creep, or over-explanation. Hard cap 350 lines; beyond that, split.

## Artefact template section name

The anatomy calls this section "Artefact template." Skills that produce a single named artefact may use a descriptive variant (e.g. "Task list template", "Finding template") — the name should identify the artefact type. The section must still appear in the required position.

## Root rules files

`PRODUCT_RULES.md`, `eng-principles-universal.md`, and `eng-principles-agentic.md` mirror the shape of their source principles documents, not this anatomy.

## Meta-pack skills

Skills with `pack: meta` are navigation and orientation artefacts, not workflow skills. They are exempt from: `principles_implemented` frontmatter, `predecessor` frontmatter, and the body sections Inputs, Outputs, Artefact template, Common rationalisations, Red flags, and Verification / exit criteria. They must still have: Title, Purpose, When to use, When not to use, and a References or equivalent lookup table.

## See also

- `docs/hook-anatomy.md` — for hooks
- `docs/sub-agent-anatomy.md` — for sub-agent personas
- `docs/brief-template.md` — for the brief that drives authoring
- `docs/authoring-learnings.md` — calibration guidance and failure modes
