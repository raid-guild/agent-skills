# RaidGuild Agent Skills

Reusable agent skills for RaidGuild.

This repo refactors the current Prism skill corpus into a smaller set of durable RaidGuild capability skills.

## Repository Layout

```text
.
├── skills/                  # Published skills after refactor and validation.
├── workflows/               # Normalized workflow recipes composed from skills.
├── references/
│   ├── writing-anti-patterns.md # Shared source material for future voice/content skills.
│   ├── prism-skills/        # Prism custom skill reference exports and migration notes.
│   └── prism-workflows/     # Prism workflow reference exports and migration notes.
├── docs/
│   ├── adopted-patterns.md  # External skill patterns adopted by this repo.
│   ├── architecture.md      # Skill design principles and boundaries.
│   ├── gaps-and-next-work.md # Remaining runtime, testing, corpus, and validation gaps.
│   ├── migration-plan.md    # Refactor workflow from Prism one-offs to repo skills.
│   ├── prism-builtin-skills.md # Prism service built-ins this repo composes with.
│   ├── refactor-plan.md     # Proposed target skill map after reviewing Prism.
│   └── voice-corpus-plan.md # Voice source strategy for RaidGuild and agent personas.
└── AGENTS.md                # Instructions for agents working in this repo.
```

## Current Phase

The first shared content slice has been created:

- `skills/rg-brand-voice`
- `skills/rg-content-strategy`
- `skills/rg-research`
- `skills/rg-public-output-safety`
- `skills/rg-publishing-ops`
- `skills/rg-portal-ops`
- `skills/rg-dao-ops`
- `skills/rg-bankr-ops`
- `skills/s3-object-storage`
- `skills/rg-media-render-ops`
- `skills/rg-crm-ops`

Next migration work:

1. Forward-test normalized workflow recipes against realistic source packages.
2. Convert accepted workflow recipes into the Prism runtime import format.
3. Enrich the first-slice references from the voice corpus and Prism workflows.

## Skill Standard

Each published skill must:

- Live in `skills/<skill-name>/`.
- Include a concise `SKILL.md` with only `name` and `description` in YAML frontmatter.
- Keep durable details in `references/` files loaded on demand.
- Own exactly one durable capability.
- Cross-reference another skill instead of duplicating its rules.
- Avoid secrets, client-private context, live credentials, and environment-specific paths.

## Candidate Capability Areas

These are planning buckets; some are now represented by first-pass skills:

- Public output safety
- RaidGuild brand and voice
- Content strategy
- Research and source discipline
- Publishing operations
- Portal and CMS operations
- CRM operations
- Object storage operations
- Media render operations
- DAO operations
- Bankr and token operations
- Skill architecture and migration

## Remote

Repository remote:

```bash
git@github.com:raid-guild/agent-skills.git
```
