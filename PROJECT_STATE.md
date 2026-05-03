# PROJECT_STATE.md

Source of truth for artefact and milestone status. Supervisor owns this file. Updated on every state transition.

Last updated: 2026-05-03 (app-calibrate skill + app-context-schema reference added)

---

## Milestone tracker

| Milestone | Description | Status |
|-----------|-------------|--------|
| M1 | Project setup complete. Repo initialised, anatomy specs accepted, `PROJECT_STATE.md` initialised. | complete |
| M2 | Root rules files accepted. `PRODUCT_RULES.md`, `eng-principles-universal.md`, `eng-principles-agentic.md` merged. | complete |
| M3 | Now complete. All 8 Now artefacts accepted, coverage matrix audit done. | complete |
| M4 | References complete. All 6 reference files merged. | complete |
| M5 | Promotion review (optional). Re-evaluate Next items against current evidence. | complete |
| M6 | Ship. All artefacts on main, project closed. | complete |

---

## Now (8 artefacts)

| # | Artefact | Category | Track | Status | Branch | Notes |
|---|----------|----------|-------|--------|--------|-------|
| 1 | `PRODUCT_RULES.md` | rules | product | accepted | — | merged PR #2 |
| 2 | `idea-triage` | skill | product | accepted | — | merged |
| 3 | `eng-principles-universal.md` | rules | engineering | accepted | — | merged PR #1 |
| 4 | `eng-principles-agentic.md` | rules | engineering | accepted | — | merged PR #3 |
| 5 | `design-doc` | skill | engineering | accepted | — | merged |
| 6 | `incremental-implementation` | skill | engineering | accepted | — | merged to main |
| 7 | `stop-the-line` | hook | hook | accepted | — | merged |
| 8 | README | meta | meta | accepted | — | rewritten M6 |
| 9 | `using-this-pack` | skill | meta | accepted | — | promoted from Next |
| 10 | `planning-and-task-breakdown` | skill | engineering | accepted | — | promoted from Next |
| 11 | `roadmap-shape` | skill | product | accepted | — | promoted from Next |
| 15 | `prototype-to-validate` | skill | engineering | accepted | — | promoted from Next |
| 16 | `backlog-manage` | skill | product | accepted | — | new skill |
| 17 | `app-calibrate` | skill | product | accepted | — | new skill; grounds idea-triage Impact scores |

---

## Next (11 artefacts)

| # | Artefact | Category | Status | Promotion criteria |
|---|----------|----------|--------|--------------------|
| 12 | `small-batch` | hook | pending | after `stop-the-line` proves failure-mode-detection pattern |
| 13 | `evidence-claim` | hook | pending | after `stop-the-line` proves failure-mode-detection pattern |
| 14 | `problem-first-reviewer` | sub-agent | pending | when `design-doc` usage shows need |
| 15 | `prototype-to-validate` | skill | accepted | promoted to Now |
| 16 | `spike` | skill | pending | capacity opens |
| 17 | `deploy` | skill | pending | capacity opens |
| 18 | `post-launch-impact-review` | skill | pending | capacity opens |
| 19 | `roadmap-review` | skill | pending | capacity opens |

---

## References (7 files)

| File | Status | Cited by |
|------|--------|----------|
| `references/confidence-meter.md` | accepted | idea-triage, roadmap-shape, post-launch-impact-review |
| `references/ice-scoring.md` | accepted | idea-triage |
| `references/kano-classification.md` | accepted | idea-triage |
| `references/portfolio-themes.md` | accepted | roadmap-shape |
| `references/nfr-categories.md` | accepted | design-doc |
| `references/dora-metrics.md` | accepted | post-launch-impact-review, deploy |
| `references/app-context-schema.md` | accepted | app-calibrate, idea-triage |

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
