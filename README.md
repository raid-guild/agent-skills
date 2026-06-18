# RaidGuild Agent Skills

Reusable agent skills for RaidGuild.

This repo is intentionally starting with **no published skills**. The first phase is to collect the current Prism skill corpus as source material, identify duplicated concepts, and refactor it into a smaller set of durable capability skills.

## Repository Layout

```text
.
├── skills/                  # Published skills. Empty until a skill is refactored and validated.
├── references/
│   └── prism-skills/        # Raw Prism skill exports and migration notes.
├── docs/
│   ├── architecture.md      # Skill design principles and boundaries.
│   └── migration-plan.md    # Refactor workflow from Prism one-offs to repo skills.
└── AGENTS.md                # Instructions for agents working in this repo.
```

## Current Phase

1. Dump the existing Prism skills into `references/prism-skills/raw/`.
2. Build an inventory in `references/prism-skills/inventory.md`.
3. Group duplicated behavior into capability owners.
4. Create only the first validated skills in `skills/`.

## Skill Standard

Each published skill must:

- Live in `skills/<skill-name>/`.
- Include a concise `SKILL.md` with only `name` and `description` in YAML frontmatter.
- Keep durable details in `references/` files loaded on demand.
- Own exactly one durable capability.
- Cross-reference another skill instead of duplicating its rules.
- Avoid secrets, client-private context, live credentials, and environment-specific paths.

## Candidate Capability Areas

These are planning buckets, not skills yet:

- Public output safety
- RaidGuild brand and voice
- Content strategy
- Research and source discipline
- Publishing operations
- Portal and CMS operations
- CRM operations
- DAO operations
- Bankr and token operations
- Skill architecture and migration

## Remote

Repository remote:

```bash
git@github.com:raid-guild/agent-skills.git
```
