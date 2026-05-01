# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---
type: Note
_organized: true
---

@AGENTS.md

---

## What this repo is

A Markdown-only skill pack — no build system, no tests, no CI. Every artefact is a `.md` file. The deliverable is well-authored prose, not runnable code.

---

## Repo structure

```
skills/
  product/          PRODUCT_RULES.md + skill subdirs (idea-triage/, roadmap-shape/)
  engineering/      eng-principles-universal.md, eng-principles-agentic.md + skill subdirs
  using-this-pack/  meta-skill
hooks/
  stop-the-line/    HOOK.md
references/         Six standalone reference files cited by skills
docs/               Anatomy specs and authoring guidance (skill-anatomy.md, hook-anatomy.md, …)
_briefs/            Author briefs (input artefacts, not shipped)
```

Skills live at `skills/<pack>/<name>/SKILL.md`. Hooks at `hooks/<name>/HOOK.md`. References at `references/<name>.md`. Root rules files (`PRODUCT_RULES.md`, `eng-principles-*.md`) are flat files, not subdirectories.

---

## Authoring a new skill

Follow `docs/skill-anatomy.md` exactly. Required sections in order: Title → Purpose → When to use → When not to use → Inputs → Outputs → Workflow → Artefact template → Common rationalisations → Red flags → Verification / exit criteria → References.

Required frontmatter fields: `name`, `description`, `pack`, `lifecycle_stage`, `principles_implemented` (each with `source`, `id`, `bucket`), `length_target`, `author`, `predecessor` (with `relation`).

Length target: 100–300 lines. Hard cap 350. Below 100 triggers under-specification check. Above 300 triggers redundancy check.

Gates in the workflow section are marked `[GATE]` — do not remove them or make them optional.

---

## Authoring a hook

Follow `docs/hook-anatomy.md`. Hooks have deterministic pass/fail criteria. Fail criteria that are non-deterministic are a reject trigger — flag and fix before shipping.

---

## PROJECT_STATE.md

Source of truth for artefact status. Update on every state transition:
- When an artefact moves from Next → Now: add a row to the Now table, update the Next table row status.
- When an artefact is accepted: set status to `accepted`, add branch `—`, add merge note.
- Update the `Last updated:` line on every change.

---

## Commit style

No `Co-Authored-By` trailers. Push directly to main — no PRs unless owner asks. Commit message format: `feat: <verb> <artefact> (<short rationale>)`.

---

## Key constraints

- No stack-prescriptive content in skill prose. Skills are stack-agnostic.
- No verbatim copy from `addyosmani/agent-skills`. Every artefact must declare its predecessor relation in frontmatter.
- Voice must match the existing skills — direct, principle-named, no generic AI filler. Read two existing SKILL.md files before authoring a new one.
- `skills/engineering/eng-principles-universal.md` is the canonical source for principle IDs cited in engineering skills. Read it before referencing any principle.
