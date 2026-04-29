# PROJECT_STATE.md

Source of truth for artefact and milestone status. Supervisor owns this file. Updated on every state transition.

Last updated: 2026-04-30 (M3: three drafts in consistency check)

---

## Milestone tracker

| Milestone | Description | Status |
|-----------|-------------|--------|
| M1 | Project setup complete. Repo initialised, anatomy specs accepted, `PROJECT_STATE.md` initialised. | complete |
| M2 | Root rules files accepted. `PRODUCT_RULES.md`, `eng-principles-universal.md`, `eng-principles-agentic.md` merged. | complete |
| M3 | Now complete. All 8 Now artefacts accepted, coverage matrix audit done. | pending |
| M4 | References complete. All 6 reference files merged. | pending |
| M5 | Promotion review (optional). Re-evaluate Next items against current evidence. | pending |
| M6 | Ship. v0.1.0 tagged, project closed. | pending |

---

## Now (8 artefacts)

| # | Artefact | Category | Track | Status | Branch | Notes |
|---|----------|----------|-------|--------|--------|-------|
| 1 | `PRODUCT_RULES.md` | rules | product | accepted | — | merged PR #2 |
| 2 | `idea-triage` | skill | product | consistency | worktree-agent-a072477db256def6f | editor accepted, no changes |
| 3 | `eng-principles-universal.md` | rules | engineering | accepted | — | merged PR #1 |
| 4 | `eng-principles-agentic.md` | rules | engineering | accepted | — | merged PR #3 |
| 5 | `design-doc` | skill | engineering | consistency | worktree-agent-a6901afbfb8e91d15 | editor added P5 to frontmatter |
| 6 | `incremental-implementation` | skill | engineering | pending | — | sequential after #5 |
| 7 | `stop-the-line` | hook | hook | consistency | worktree-agent-a46329fb876c35835 | editor added non-blocking statement |
| 8 | README routing section | meta | meta | pending | — | owner work, M6 |

---

## Next (11 artefacts)

| # | Artefact | Category | Status | Promotion criteria |
|---|----------|----------|--------|--------------------|
| 9 | `using-this-pack` | skill | pending | capacity opens, pack grows |
| 10 | `planning-and-task-breakdown` | skill | pending | capacity opens |
| 11 | `roadmap-shape` | skill | pending | capacity opens, bootstrapping argument strengthened |
| 12 | `small-batch` | hook | pending | after `stop-the-line` proves failure-mode-detection pattern |
| 13 | `evidence-claim` | hook | pending | after `stop-the-line` proves failure-mode-detection pattern |
| 14 | `problem-first-reviewer` | sub-agent | pending | when `design-doc` usage shows need |
| 15 | `prototype-to-validate` | skill | pending | capacity opens |
| 16 | `spike` | skill | pending | capacity opens |
| 17 | `deploy` | skill | pending | capacity opens |
| 18 | `post-launch-impact-review` | skill | pending | capacity opens |
| 19 | `roadmap-review` | skill | pending | capacity opens |

---

## References (6 files)

| File | Status | Cited by |
|------|--------|----------|
| `references/confidence-meter.md` | pending | idea-triage, roadmap-shape, post-launch-impact-review |
| `references/ice-scoring.md` | pending | idea-triage |
| `references/kano-classification.md` | pending | idea-triage |
| `references/portfolio-themes.md` | pending | roadmap-shape |
| `references/nfr-categories.md` | pending | design-doc |
| `references/dora-metrics.md` | pending | post-launch-impact-review, deploy |

---

## Status definitions

| Status | Meaning |
|--------|---------|
| `pending` | Not yet started |
| `pending-review` | Draft exists; skipped authoring (fast-path); queued for editor |
| `brief-ready` | Brief written and committed |
| `in-progress` | Author has the draft |
| `editorial` | Editor reviewing |
| `consistency` | Consistency checker reviewing |
| `owner-review` | PR open, awaiting owner sign-off |
| `accepted` | Merged to main |
| `blocked` | Blocked — see Notes |
