# pde-skills — Project Governance

Companion to `PROJECT_PLAN.md`. The plan covers what gets built and how, in language an executing agent uses. This file covers strategic framing, audit criteria, and decision rationale — the content the owner needs to track project health and make replanning decisions, but agents executing the build don't.

---

## 1. Strategic goals

The project produces a product-design-engineering skill pack for use with agentic coding and PM tools, structured so that:

1. **The owner uses it personally first** — every artefact must work for a single PM/engineer-of-one before it works for a team.
2. **It scales to a small team** — naming, structure, and dependencies are clean enough that a team adopting it doesn't need to refactor.
3. **It ships open-source from day one** — public, MIT-licensed, contribution-ready, explicit credit to addyosmani/agent-skills.
4. **It is a meaningful improvement on prior art** — covers ground addy's pack misses or covers it differently because the owner's principles demand it.

Owner framing: this pack is built by an engineer who also does PM work, not a PM with an engineering background. Engineering is home territory; the product pack closes the deciding loop that engineering alone leaves open.

---

## 2. Owner-decision non-goals

- **Trial use during the project.** Owner trials post-ship for ~2 weeks and feeds learnings into v0.2. v0.1 success is judged on artefacts, not usage outcomes.
- **Design pack** — deferred until design principles are drafted.
- **Hard fork** — soft fork only; separate repo, no inherited history, attribution by reference.
- **Visual identity / branding** — no logo, no marketing site.
- **Automated CI testing of skills** — QA pipeline is human-and-agent review.

(Agent-actionable non-goals are in `PROJECT_PLAN.md` §2.)

---

## 3. OKRs

OKRs focus on artefact quality, shippability, and honest relationship to prior art. Usage-based outcomes are excluded — they belong to v0.2. Most editor-actionable items have been promoted into the editor's reject triggers in `PROJECT_PLAN.md` §6.3; what remains here is owner-audit content.

### Objective 1 — The pack is internally coherent and principle-aligned

| KR | Measurement |
|---|---|
| 1.1 — Every artefact traces to ≥1 named principle, with bucket assignment | Cross-pack consistency check; many-to-many tracing |
| 1.2 — Every principle has ≥1 artefact operationalising it (any bucket), OR explicit "intentionally not yet operationalised" entry | Coverage matrix audit at M5 |
| 1.3 — No two artefacts duplicate the same workflow | Editor cross-pack pass |
| 1.4 — Voice consistency across artefacts | Editorial QA |
| 1.5 — Each artefact has explicit "when to use / when not to use" guidance | Editor check |
| 1.6 — Embedded-everywhere principles name three load-bearing homes each | Editor check at M3 |

Known carve-outs at M5: Eng Universal Principle 1 (outcome verification), Roadmap 10 and Eng Rule D2 (learning-loop principles). Each is intentionally left to v0.2 because the validating skills are in Next.

### Objective 2 — The pack honestly relates to prior art

| KR | Measurement |
|---|---|
| 2.1 — Every artefact declares its relationship to addy's pack | Frontmatter audit |
| 2.2 — Artefacts with predecessors name what was kept and what was changed | Editor check |
| 2.3 — Attribution is present and accurate in README | Final integration check |
| 2.4 — No copy-paste from addy's content | Editor spot check |

### Objective 3 — The pack is shippable open-source

| KR | Measurement |
|---|---|
| 3.1 — All Now items pass QA | `accepted` state in review file |
| 3.2 — Repo has license, README, contribution guide | Final integration check |
| 3.3 — Owner can hand the repo to a stranger and they can use it | Walkthrough by an unfamiliar reader (fresh agent session) |
| 3.4 — README carries the size-the-work rubric as canonical home for v0.1 | Final integration check |

### Objective 4 — The pack is iterable post-v0.1

| KR | Measurement |
|---|---|
| 4.1 — Change-log discipline established | `CHANGELOG.md` v0.1.0 entry; `CONTRIBUTING.md` describes revision flow |
| 4.2 — Iteration scaffolding in place | `LEARNINGS.md` and `POST_V0.1_BACKLOG.md` populated |

---

## 4. Failure conditions (project is failing if)

- Artefact voice reads as generic AI output rather than matching the source docs.
- Cross-artefact redundancy or contradiction lands in v0.1.
- Any artefact fails to trace to a named principle and ships anyway.
- Stack-prescriptive content slips past editorial review.
- A principle has no artefact operationalising it (any bucket) and the absence isn't documented.
- An artefact has a clear predecessor in addy's pack but the relationship isn't declared.
- The pack reads as a rename-and-ship of addy's work rather than meaningful improvement.
- The pack implies all work goes through all skills (failure to honour KTLO and small-work carve-outs).
- Now items expand beyond the committed set without offsetting cuts.
- A hook ships with non-deterministic fail criteria.
- A sub-agent ships without an explicit "review posture" stating its stance.

---

## 5. Owner role and bottleneck management

**Responsibilities:** final acceptance on every artefact, brief approval (substance from owner, drafting by agents — see `PROJECT_PLAN.md` §10), escalation resolution, PR merges, final integration sign-off, answering questions when authors and editors hit decisions only the owner can make.

**What the owner does NOT do:** draft briefs in YAML, author skill prose, perform editorial review, run consistency checks. Those are agent responsibilities. Owner attention is spent on substance and approval, not on form.

**Bottleneck management:** owner attention is the only role that doesn't parallelise.

- **Batch by activity type.** Fixed windows for brief approval; fixed windows for PR sign-off. Don't context-switch between approving a brief and reviewing a different artefact's PR.
- **Front-load substance for independent briefs.** For artefacts whose briefs don't depend on prior accepted artefacts, the owner can convey substance to the supervisor in advance pairs:
  - `PRODUCT_RULES.md` and `eng-principles-universal.md` (no dependencies on each other; both fast-path)
  - `idea-triage` and `design-doc` (after their respective rules files are accepted)
  - `stop-the-line` (after `eng-principles-agentic.md` is at draft stage)

**Authoring context:** agents do the work, the owner is the bottleneck. Calendar appetite is not the right circuit breaker — token budget, agent rounds, and owner review attention are. Budgets: max 3 editorial rounds per artefact, ~5 agent turns per artefact on average.

---

## 6. Milestone audit detail

Per-milestone closure criteria.

### M1 — Project setup
- [ ] Repo `pde-skills` initialised, public, MIT licensed.
- [ ] `README.md` skeleton with attribution paragraph and size-the-work rubric.
- [ ] `docs/skill-anatomy.md`, `docs/hook-anatomy.md`, `docs/sub-agent-anatomy.md` accepted.
- [ ] `docs/brief-template.md`, `docs/authoring-learnings.md` accepted.
- [ ] `PROJECT_STATE.md` initialised with all 19 artefacts (8 Now, 11 Next) + 6 references.
- [ ] `hooks/` and `agents/` directories created (latter empty in v0.1).
- [ ] All agent roles configured and tested on a throwaway hello-world artefact.

### M2 — Root rules files accepted
- [ ] `PRODUCT_RULES.md` merged.
- [ ] `eng-principles-universal.md` merged.
- [ ] `eng-principles-agentic.md` merged (sequential after universal).

### M3 — Now complete
- [ ] All 5 remaining Now artefacts accepted.
- [ ] Coverage matrix audit: every Now artefact traces to ≥1 principle with bucket.
- [ ] Embedded-everywhere principles name three load-bearing homes (KR1.6).
- [ ] Predecessor declarations verified honest.
- [ ] Size-the-work rubric canonical in `README.md`.

### M4 — References complete
- [ ] All 6 reference files merged.
- [ ] Skills updated to cite them where relevant.

### M5 — Promotion review (optional)
- [ ] Re-evaluate Next items against current evidence.
- [ ] Cross-pack consistency audit across full set + 6 references.
- [ ] Coverage matrix re-audited.
- [ ] Predecessor declarations audited.

### M6 — Ship
- [ ] `CHANGELOG.md` v0.1.0 entry.
- [ ] `CONTRIBUTING.md` written.
- [ ] `LEARNINGS.md` populated.
- [ ] `POST_V0.1_BACKLOG.md` written with Later items + design-pack placeholder.
- [ ] README finalised.
- [ ] Final integration pass complete.
- [ ] Repo tagged `v0.1.0`.

---

## 7. Risks

| Risk | Mitigation |
|---|---|
| Voice drift across artefacts | Editor's voice match check; consistency checker batches voice comparisons; sequential within discipline |
| Jargon-as-rigor in prose | Editor reject trigger; flagged as v0.1 voice failure mode |
| Cross-artefact redundancy | Consistency checker pass after every accept; explicit `Out of scope` sections |
| Stack creep from addy's pack | Editor reject trigger; placeholder convention enforced |
| Skills bloat past 300 lines | Length flag; hard cap 350; split rule |
| Hook bloats into a skill | Length flag at 100 lines; reject if fail criteria not deterministic |
| Hooks ship without runtime verification of catch-rate | Acknowledged non-goal: v0.2 work |
| `agents/` ships empty | Acknowledged in repo structure as honest signalling |
| Embedded-everywhere principles become nobody's responsibility | KR1.6 audit at M3 |
| Author agent context-rot on long projects | Owner-imposed context limits; restart authors per-artefact |
| Editor becomes bottleneck | One artefact at a time; supervisor escalates |
| Owner becomes bottleneck | Batch by activity type; front-load independent briefs |
| Pack reads as rename of addy's work | Predecessor declarations mandatory; copy-paste auto-rejected; KR2 audit |
| Artefacts imply all work runs every artefact | Size-the-work rubric in README; reject if silent on triggers |
| Now expands beyond 8 without offsetting cuts | Roadmap Rule C1: appetite is a cap |
| Next items promoted without re-evaluating evidence | Promotion criteria in plan |
| Two-tier engineering principles drift if authored in parallel | Sequential authoring enforced |
| Artefacts don't survive contact with reality post-v0.1 | Expected; LEARNINGS.md and CHANGELOG.md make iteration cheap |
| Supervisor agent loses track of state | `PROJECT_STATE.md` source of truth; commit-based recovery |

---

## 8. Triage record rationales

Compressed evidence basis is in `PROJECT_PLAN.md` §11. Full prose rationales below.

### 8.1 Now items

1. **`PRODUCT_RULES.md`** — Source content exists; reformatting work; load-bearing for trace integrity across product track.

2. **`idea-triage`** — Strong principle backing (Roadmap 3, 4, 5 + Rules A2, A3, B6); v0.1 scoping conversation itself demonstrated the need; gates the product loop.

3. **`eng-principles-universal.md`** — Source content exists in `eng_principles`; reformatting + tier-1 carve-out work. Two-tier split was the highest-confidence work surfaced in v0.1 scoping.

4. **`eng-principles-agentic.md`** — Tier-2 principles derived in scoping conversation: context-as-asset, hallucination-default, evidence-beats-vibes, rationalisations-predictable, stop-the-line, memory-in-artefacts. Sequential dependency on universal.

5. **`design-doc`** — Personal usage on real work; skill formalises existing practice with NFR-numbers gate and operability section additions. Load-bearing for ~6 universal-tier principles routing through it.

6. **`incremental-implementation`** — Personal usage of addy's version; most-fired skill in the pack; refinement adds walking-skeleton-first.

7. **`stop-the-line` (hook)** — Felt-pain evidence: agents will absolutely `any`-cast, `.skip` tests, suppress lints to claim success. Mechanical failure modes, deterministic checks. Highest-confidence hook because failure modes are well-known and personal.

8. **README routing section** — Replaces `using-this-pack` skill in v0.1. With only 5 skills + 2 principles files + 1 hook, a router skill is over-scoped. README paragraph is sufficient.

### 8.2 Next items

9. **`using-this-pack`** — Cut from Now to make room for principles split. Promotes when pack has enough artefacts that README routing isn't sufficient (~8 skills).

10. **`planning-and-task-breakdown`** — Cut from Now: parallel-agent dispatch is a team-shape concern; engineer-of-one mostly runs `incremental-implementation` directly. Promotes when team-shape changes or parallel work becomes routine.

11. **`roadmap-shape`** — Cut from Now: bootstrapping argument was already weak; weakened further under pressure from new Now items. The act of placing items into a roadmap is being demonstrated *in this conversation* — the artefact lags the practice. Promotes when trial period generates enough new candidates to need formal placement.

12. **`small-batch` (hook)** — Mechanical: PR size, file count, days-since-branch — all measurable. Mixed personal usage depending on agent setup. Promote after `stop-the-line` proves the hook pattern works.

13. **`evidence-claim` (hook)** — Mechanical: scan completion claims for specific evidence references (test names, log lines, output). Mixed personal usage. Promote after `stop-the-line`.

14. **`problem-first-reviewer` (sub-agent)** — Concept-level only; no personal usage of sub-agent reviews yet. The first sub-agent earns its slot only after `design-doc` has enough usage to know whether the embedded constraint catches problem-first violations on its own.

15. **`prototype-to-validate`** — Recent personal usage ("I've been using it a lot"); fills the gap between `idea-triage` and `design-doc`; risk: don't let it grow into a UI-craft skill.

16. **`spike`** — Principle-backed (Eng Universal 4, Rules B2/C5); informal personal usage; new is the "written recommendation at expiry" discipline.

17. **`deploy`** — Necessary for end-to-end pack coherence; lower confidence than expected because full discipline (esp. error budgets) isn't current personal practice. Brief should flag aspirational vs codifying-existing-practice components.

18. **`post-launch-impact-review`** — Highest principle-weight in engineering pack (Eng Universal 1), lowest personal evidence. Authoring posture: first run is v0.2 scoping; if it doesn't help, kill or reshape.

19. **`roadmap-review`** — Same shape as `post-launch-impact-review` for the product track. Closes the learning loop addy's pack leaves open at the portfolio level.

### 8.3 Later items (deferred with rationale)

Each captures evidence for *why* it's not in v0.1.

**Skill candidates:**
- `adr` — descoped on personal-usage evidence: "almost never used"
- `debugging-and-error-recovery` — descoped on personal-usage evidence: "never used"
- `code-review-and-quality` — descoped to author later; agent-loop fit high but timing wasn't right
- `cross-team-dependency-surfacing` — low fit for engineer-of-one; high fit when team adopts
- `fitness-functions`, `boring-technology`, `blameless-postmortem`, `build-vs-buy-vs-adopt`, `error-budgets`, `platform-as-product`, `engineering-decision-retrospective`, `pm-decision-retrospective` — principle-backed, low personal practice
- TDD, security, accessibility, perf, git-workflow, ci-cd as standalones — currently folded into Now skills; promote to standalones if v0.1 trial shows the fold isn't carrying its weight

**Hook candidates:**
- `artefact-pair` (confidence 2) — flag code change without doc/ADR update; depends on artefact discipline being real first
- `hallucination-citation` (confidence 3) — flag framework/library claims without source citation; promote after `stop-the-line` and `evidence-claim` prove hooks work

**Sub-agent persona candidates:**
- `novelty-justification-reviewer` (confidence 1.5) — validates boring-tech compliance
- `security-and-sensitivity-reviewer` (descoped) — security review without real personal usage and codebase will perform worse than no skill at all. Theatre risk too high.
- `hallucination-verifier` (confidence 1.5) — counterpart to citation hook; promotes only after hook proves failure-mode is real

**Discipline:**
- All design-pack skills — awaiting design principles draft

---

## 9. Deliverables checklist (project closure at M6)

- [ ] 5 Now skill files merged: `idea-triage`, `design-doc`, `incremental-implementation`
- [ ] 3 root rules files: `PRODUCT_RULES.md`, `eng-principles-universal.md`, `eng-principles-agentic.md`
- [ ] 1 hook: `stop-the-line` under `hooks/stop-the-line/HOOK.md`
- [ ] README routing section merged into `README.md`
- [ ] Any Next items promoted during the cycle, merged
- [ ] 6 `references/*.md` files merged
- [ ] `README.md` complete with attribution and size-the-work rubric
- [ ] `LICENSE` (MIT) in place
- [ ] `CONTRIBUTING.md` written
- [ ] `CHANGELOG.md` v0.1.0 entry
- [ ] `LEARNINGS.md` populated with v0.1 authoring learnings, ready for trial findings
- [ ] `POST_V0.1_BACKLOG.md` written
- [ ] `docs/skill-anatomy.md`, `docs/hook-anatomy.md`, `docs/sub-agent-anatomy.md`, `docs/brief-template.md`, `docs/authoring-learnings.md` finalised
- [ ] `hooks/` populated; `agents/` present (empty in v0.1)
- [ ] Coverage matrix audit complete
- [ ] Embedded-everywhere principles each name three load-bearing homes
- [ ] Predecessor declarations honest across all artefacts
- [ ] Size-the-work rubric canonical in `README.md`
- [ ] No artefact in any state other than `accepted`, explicitly promoted, or explicitly carried to v0.2
- [ ] All `_workspace/` directories deleted

---

## 10. Post-ship plan

Not part of this project. Owner trials the pack on real PM/engineering work for ~2 weeks following M6. Findings logged to `LEARNINGS.md`. v0.2 scoping happens after the trial period based on `LEARNINGS.md` content. Likely v0.2 scope: design pack (once design principles are drafted), Next-item promotions that didn't happen in v0.1, refinements to v0.1 artefacts, candidates from Later set surfaced by trial.

This project ends at M6.

---

## 11. Plan version history

- **v1.6** — Owner role corrected. Briefs are agent-drafted and owner-approved, not owner-authored. Workflow gains a fast-path variant for artefacts whose substance is already settled (v0.1 rules files derived from existing principles documents). Plan §5.1, §6.2, §7, §10 updated accordingly. Governance §5 (owner role) reflects the actual owner contribution: substance and approval, not drafting. The two engineering principles files (`eng-principles-universal.md`, `eng-principles-agentic.md`) generated as part of this revision and slotted directly under `skills/engineering/` — they take the fast-path workflow on first authoring.

- **v1.5** — Split into PROJECT_PLAN.md (operational spine) and PROJECT_GOVERNANCE.md (this file). Anatomy specs, brief template, and authoring learnings extracted to `docs/`. Editor-actionable OKR content promoted into `PROJECT_PLAN.md` §6.3 reject triggers. Net effect: agents executing the build load only operational content; owner-facing material lives where the owner reads it. Total content ~50% of v1.4 size in the file an executing agent loads.

- **v1.4** — Engineering principles split into two tiers (universal / agentic) reflected in the roadmap. New artefact categories added: hooks (failure-mode-detection) and sub-agent personas (adversarial review). Now stays at 8 items but composition changes: `ENGINEERING_RULES.md` → `eng-principles-universal.md` + `eng-principles-agentic.md`; add `stop-the-line` hook; cut `roadmap-shape`, `using-this-pack`, `planning-and-task-breakdown` to Next. Repo structure adds `hooks/` and `agents/`. Anatomy frontmatter extended for multi-tier principle tracing with bucket assignment.

- **v1.3** — Skill list rebuilt around lifecycle (Define/Plan/Build/Ship/Verify). Phase 1/Phase 2/Phase 3 → Now/Next/Later. 13 items total (8 Now, 5 Next). Removed `adr`, `debugging-and-error-recovery`, `code-review-and-quality`, `cross-team-dependency-surfacing`. Added `prototype-to-validate`. Added §13 triage records.

- **v1.2** — Predecessor mapping made explicit; `idea-triage` absorbs roadmap-item-framing; `using-this-pack` carries the size-the-work rubric.
