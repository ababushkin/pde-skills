# pde-skills

Workflow skills for the small product-design-engineering team — including the team of one.

## Attribution

This pack is a soft fork of [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) by Addy Osmani. It inherits the structural conventions (skill frontmatter, anatomy specs, the `SKILL.md` pattern) and improves on them where the owner's principles demand. Where an artefact has a counterpart in addy's pack, the relationship is declared explicitly in the artefact's frontmatter (`predecessor`, `kept_from_predecessor`, `changed_from_predecessor`). Where an artefact is new, it stands alone. No paragraph in this pack is a verbatim copy of the source.

## How to size the work

<!-- SIZE-THE-WORK RUBRIC — PLACEHOLDER: AWAITING OWNER CANONICAL WORDING -->

## What's in the pack

The pack ships three artefact categories:

- **Skills** — workflows agents invoke when triggered.
- **Hooks** — mechanical checks that run on events (commit, PR, completion claim) to catch failure modes the agent has every reason not to flag against itself.
- **Sub-agent personas** — adversarial review passes with fresh context and no investment in the original work.

See `docs/skill-anatomy.md`, `docs/hook-anatomy.md`, and `docs/sub-agent-anatomy.md` for authoring specs.

## Repository layout

```
pde-skills/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── CHANGELOG.md
├── LEARNINGS.md
├── POST_V0.1_BACKLOG.md
├── PROJECT_PLAN.md
├── PROJECT_STATE.md
├── docs/
│   ├── skill-anatomy.md
│   ├── hook-anatomy.md
│   ├── sub-agent-anatomy.md
│   ├── brief-template.md
│   └── authoring-learnings.md
├── references/
├── skills/
│   ├── product/
│   └── engineering/
├── hooks/
└── agents/
```

## License

MIT — see [LICENSE](LICENSE).
