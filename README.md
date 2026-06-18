# RaidGuild Agent Skills

Reusable agent skills for RaidGuild.

This repo refactors the current Prism skill corpus into a smaller set of durable RaidGuild capability skills.

## Repository Layout

```text
.
├── skills/                  # Published skills after refactor and validation.
├── references/
│   ├── writing-anti-patterns.md # Shared source material for future voice/content skills.
│   ├── prism-skills/        # Prism custom skill reference exports and migration notes.
│   └── prism-workflows/     # Prism workflow reference exports and migration notes.
├── docs/
│   ├── adopted-patterns.md  # External skill patterns adopted by this repo.
│   ├── architecture.md      # Skill design principles and boundaries.
│   ├── migration-plan.md    # Refactor workflow from Prism one-offs to repo skills.
│   ├── refactor-plan.md     # Proposed target skill map after reviewing Prism.
│   └── voice-corpus-plan.md # Voice source strategy for RaidGuild and agent personas.
└── AGENTS.md                # Instructions for agents working in this repo.
```

## Current Phase

The first shared content slice has been created:

- `skills/rg-brand-voice`
- `skills/rg-content-strategy`
- `skills/rg-public-output-safety`
- `skills/rg-publishing-ops`
- `skills/portal-ops`
- `skills/rg-dao-ops`
- `skills/rg-bankr-ops`

Next migration work:

1. Enrich the first-slice references from the voice corpus and Prism workflows.
2. Forward-test content, publishing, and Portal flows on realistic Queen Raida, AI Solutions, and public RaidGuild tasks.
3. Refactor CRM, media, and arcade/reporting operations next.

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
- DAO operations
- Bankr and token operations
- Skill architecture and migration

## Remote

Repository remote:

```bash
git@github.com:raid-guild/agent-skills.git
```
