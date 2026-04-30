# pde-skills

**Workflow skills for a the small product-design-engineering team - including the team of one.**

Skills encode the discipline that experienced PDE teams apply at each decision point: which ideas to pursue, how to structure work, how to build it, and how to catch failure modes before they compound. Packaged so AI agents follow them consistently instead of taking shortcuts.

```
  DISCOVER         DECIDE          DESIGN            BUILD
 ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
 │  idea    │──▶ │  roadmap │──▶ │ design   │──▶ │  incr.   │
 │  triage  │    │  shape   │    │  doc     │    │  impl.   │
 └──────────┘    └──────────┘    └──────────┘    └──────────┘
                                                       ▲
                                                 planning &
                                               task breakdown
```

---

## When to use which skill

| You're doing this | Use this |
|---|---|
| An idea arrives — worth pursuing? | [`idea-triage`](skills/product/idea-triage/SKILL.md) |
| Planning cycle — what to build next? | [`roadmap-shape`](skills/product/roadmap-shape/SKILL.md) |
| Significant engineering work — how to build it? | [`design-doc`](skills/engineering/design-doc/SKILL.md) |
| Have a design — break it into tasks | [`planning-and-task-breakdown`](skills/engineering/planning-and-task-breakdown/SKILL.md) |
| Building anything non-trivial | [`incremental-implementation`](skills/engineering/incremental-implementation/SKILL.md) |
| Fixing a bug | [`incremental-implementation`](skills/engineering/incremental-implementation/SKILL.md) bug-fix sub-workflow |
| Agent says it's done | [`stop-the-line`](hooks/stop-the-line/HOOK.md) fires automatically |

---

## Skills

### Product

| Skill | What it does | Use when |
|---|---|---|
| [PRODUCT_RULES.md](skills/product/PRODUCT_RULES.md) | Rule set covering idea filtering (P2–P4), roadmap discipline (B1–B5), and capacity allocation (C1–C3). | Load persistently for product work |
| [idea-triage](skills/product/idea-triage/SKILL.md) | Interrogates incoming ideas through confidence gates, ICE scoring, and Kano classification. Routes to: build, validate, defer, or discard. | Any proposal arrives |
| [roadmap-shape](skills/product/roadmap-shape/SKILL.md) | Builds a roadmap using portfolio-theme classification and explicit capacity allocation. Names the implicit portfolio mix before committing. | Planning cycle; roadmap review |

### Engineering

| Skill | What it does | Use when |
|---|---|---|
| [eng-principles-universal.md](skills/engineering/eng-principles-universal.md) | Rule set: design before build (A1–A5), small batch (B1), explicit contracts (C1–C3), technical quality (D1–D4). | Load persistently for engineering work |
| [eng-principles-agentic.md](skills/engineering/eng-principles-agentic.md) | Agentic-specific constraints: scope discipline, no speculative refactoring, confirmation before destructive action. | Load alongside universal for agent-driven work |
| [planning-and-task-breakdown](skills/engineering/planning-and-task-breakdown/SKILL.md) | Decomposes a design doc or spec into small, verifiable tasks with acceptance criteria and dependency order. | Design accepted; ready to implement |
| [design-doc](skills/engineering/design-doc/SKILL.md) | Structures significant work before building: problem statement, approach options, chosen design, NFR constraints, operability plan. | Work exceeds 4 weeks, reused capability, or meaningful user/cost/compliance impact |
| [incremental-implementation](skills/engineering/incremental-implementation/SKILL.md) | Thin vertical slices — implement, test, verify, commit. Walking skeleton first. Bug-fix sub-workflow for KTLO work. | Building anything touching more than one file |

---

## Hooks

Hooks are mechanical checks that fire on events. They catch failure modes the agent has every reason not to flag against itself.

| Hook | What it catches | Fires when |
|---|---|---|
| [stop-the-line](hooks/stop-the-line/HOOK.md) | Type suppressions, compiler directives, test skips, deleted assertions, static-analysis suppressions in a diff | Agent signals work is done |

---

## References

Short reference files cited by skills. Load on demand.

| Reference | What it contains | Cited by |
|---|---|---|
| [confidence-meter](references/confidence-meter.md) | Gilad 1–5 evidence quality scale | idea-triage, roadmap-shape |
| [ice-scoring](references/ice-scoring.md) | ICE = Impact × Confidence × Ease formula and scoring guide | idea-triage |
| [kano-classification](references/kano-classification.md) | Five-category feature taxonomy (must-be → excitement) with decay behaviour | idea-triage |
| [portfolio-themes](references/portfolio-themes.md) | Doshi's seven strategic themes with capacity allocation guidance | roadmap-shape |
| [nfr-categories](references/nfr-categories.md) | NFR taxonomy: category, measurable target, fitness function type | design-doc |
| [dora-metrics](references/dora-metrics.md) | Four DORA metrics with elite / high / medium / low benchmarks | post-launch-impact-review, deploy |

---

## How to install

Skills are plain Markdown. Load them via `AGENTS.md`, `CLAUDE.md`, or your agent's system-prompt mechanism.

**Claude Code — add `@` references to your project's `AGENTS.md`:**

```
# Rule files — load persistently
@path/to/pde-skills/skills/product/PRODUCT_RULES.md
@path/to/pde-skills/skills/engineering/eng-principles-universal.md
@path/to/pde-skills/skills/engineering/eng-principles-agentic.md

# Skills — load situationally
# @path/to/pde-skills/skills/product/idea-triage/SKILL.md
# @path/to/pde-skills/skills/engineering/design-doc/SKILL.md
```

Load rule files persistently. Load skills situationally — only the ones relevant to the current session. Loading all skills at once wastes context.

**Cursor, Gemini CLI, Windsurf, other agents:**

Paste the content of the relevant `SKILL.md` or rule file into your agent's rules/instructions file for the project.

---

## How to size the work

Size the work before you start.

| Size | Complexity | Changes expected | Input required from you |
|------|------------|-----------------|------------------------|
| Small | Single concern, clear scope | Few files, low risk of cascades | Little to none — agent executes, you review output |
| Medium | Multiple concerns or uncertain scope | Moderate changes, some coordination | Occasional decisions; expect 1–2 rounds |
| Large | High complexity, cross-cutting, or contested tradeoffs | Many changes, likely revisions | Heavy involvement — frame the problem, review drafts, resolve conflicts |

Skills declare which sizes they apply to. When a skill fires on work that's larger than its declared size, stop and split the work first.

---

## Attribution

This pack is a soft fork of [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) by Addy Osmani. It inherits the structural conventions (skill frontmatter, anatomy specs, the `SKILL.md` pattern) and improves on them where the owner's principles demand. Where an artefact has a counterpart in addy's pack, the relationship is declared explicitly in the artefact's frontmatter (`predecessor`, `kept_from_predecessor`, `changed_from_predecessor`). Where an artefact is new, it stands alone. No paragraph in this pack is a verbatim copy of the source.

---

## License

MIT — see [LICENSE](LICENSE).
