# Prism Skill Migration Plan

Use this process to refactor current Prism skills into a smaller RaidGuild skill system.

See `docs/refactor-plan.md` for the current proposed target skill map.

## Phase 1: Collect

Dump current Prism skills into one folder per skill:

```text
references/prism-skills/<prism-skill-name>/SKILL.md
```

Dump current Prism workflow references into:

```text
references/prism-workflows/
```

Keep the exported `SKILL.md` as the source reference for migration. If a later export includes additional files, keep those files inside the same skill folder:

```text
references/prism-skills/<prism-skill-name>/
```

If only descriptions are available, add them to `references/prism-skills/inventory.md`.

For workflows, prefer one folder per workflow with a normalized manifest, workflow markdown, step markdown, and source metadata:

```text
references/prism-workflows/<workflow-key>/
├── manifest.proposal.json
├── workflow.md
├── source.json
└── steps/
```

## Phase 2: Inventory

For each Prism skill, record:

- Current name
- Current trigger description
- Primary behavior
- Tool or system dependencies
- Safety concerns
- Proposed owner capability
- Migration decision

Migration decisions:

- `keep`: remains a standalone skill
- `merge`: absorbed into a capability skill
- `reference`: becomes a reference file, template, or persona profile
- `deprecate`: remove after replacement exists
- `unknown`: needs review

## Phase 3: Group

Group skills by durable capability, not by current agent name.

Initial grouping candidates:

- Public output safety
- Brand and voice
- Content strategy
- Research
- Publishing operations
- Portal/CMS operations
- CRM operations
- DAO operations
- Bankr/token operations
- Game/reporting operations

## Phase 4: Design Owners

For each candidate owner skill, define:

- What it owns
- What it explicitly does not own
- Which Prism skills it absorbs
- Which references it needs
- Which other skills it must call or cross-reference

## Phase 5: Create Skills

Only create a skill in `skills/` after the boundary is clear.

Each skill should start with:

```text
skills/<skill-name>/
├── SKILL.md
└── references/
```

Add scripts or assets only when needed.

## Phase 6: Validate

Validate each skill on realistic tasks before treating it as published.

For content skills, use real draft inputs with sensitive details removed.
For ops skills, prefer read-only or dry-run tasks first.
For financial, governance, wallet, publishing, or client-impacting operations, require explicit human approval before live actions.
