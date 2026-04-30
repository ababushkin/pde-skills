---
name: using-this-pack
description: >
  Meta-skill for navigating pde-skills. Identifies which skill applies to the current task
  and explains the core operating behaviours that apply across all skills. Load at session
  start or when uncertain which skill to invoke.
pack: meta
lifecycle_stage: all
length_target: 120–160
author: Anton Babushkin
---

# Using this pack

## Purpose

This skill is the entry point to pde-skills. It answers "which skill should I invoke right now?" and defines the operating behaviours that apply to every skill in the pack. Load it at the start of a product or engineering session, or when you're uncertain which skill fires for the current task.

## Skill discovery

Identify the current task and follow the first matching branch.

```
Task arrives
    │
    ├── An idea or request arrived — worth pursuing?       → idea-triage
    ├── Building or reviewing a roadmap?                   → roadmap-shape
    ├── Significant engineering work — how to build it?   → design-doc
    ├── Have a design or spec — need implementable tasks?  → planning-and-task-breakdown
    ├── Ready to build?                                    → incremental-implementation
    │   └── KTLO bug fix (no design doc)?                 → incremental-implementation (Path 2)
    └── Agent signals it's done?                          → stop-the-line (hook — fires on claims)
```

Rules and references are not skills — they are loaded as context.

| Load this | When |
|---|---|
| `PRODUCT_RULES.md` | Any product decision, roadmap work, idea evaluation |
| `eng-principles-universal.md` | Any engineering design or build work |
| `eng-principles-agentic.md` | Any agent-driven engineering work (alongside universal) |
| Reference files | When a skill explicitly invokes one |

## Core operating behaviours

These apply across every skill in the pack. They are not optional.

**Surface assumptions before acting.** Before any non-trivial action, state the assumptions being made and give the owner a chance to correct them. Wrong assumptions caught early are cheap; wrong assumptions caught after implementation are expensive.

**Stop at gates.** Each skill contains numbered gates (`[GATE]`). A gate is a hard stop — do not proceed past it until the gate condition is met. Gates exist because the work that follows them is wasted if the gate condition is false.

**Scope discipline.** Touch only what the current skill requires. Do not refactor adjacent code, remove things you don't understand, or add features not in the spec. Every deviation from scope requires explicit owner approval.

**Confirm before destructive action.** Deletion, reset, overwrite, force-push, dropping a table — pause and confirm with the owner before proceeding. The cost of confirmation is one message; the cost of an unintended destructive action can be days of recovery.

**Incomplete is not done.** A task is not complete until its verification criteria pass. "Seems right" is never sufficient. Evidence is required: passing tests, build output, measurement.

**Disagreement is required.** If an approach has a clear problem, name it, quantify the downside, and propose an alternative. Accept the owner's final decision. Sycophantic agreement with a bad plan is a worse failure mode than honest pushback.

## Common mistake: skipping skills

Skills are not ceremony — they encode the checks that prevent the most common and expensive failure modes. Skipping idea-triage produces a roadmap full of unvalidated opinions. Skipping design-doc produces implementations that solve the wrong problem or the right problem in an unmaintainable way. Skipping planning-and-task-breakdown produces an implementation plan that falls apart at the first unexpected dependency.

The value of a skill is highest the first time you skip it and something breaks. After that, the cost of not skipping it is obvious.

## Quick reference

| Skill | Trigger phrase | Key output |
|---|---|---|
| `idea-triage` | "We should build…", "A customer asked for…", "Competitor just launched…" | Triage record with ICE score and routing decision |
| `roadmap-shape` | "Let's do planning", "What should we build next?", "Review the roadmap" | Shaped Now/Next/Later roadmap with explicit capacity allocation |
| `planning-and-task-breakdown` | "Design is accepted — let's implement", "Break this down into tasks" | Ordered task list with acceptance criteria |
| `design-doc` | "How should we build X?", work exceeds 4 weeks, capability will be reused | Accepted design doc |
| `incremental-implementation` | "Let's build", "Start implementing" | Working slice committed to main |
| `stop-the-line` | "I'm done", "All done", "Completed" | Completion verified or halt raised |
