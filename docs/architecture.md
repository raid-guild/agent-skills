# Skill Architecture

RaidGuild skills should be small, composable capability modules. The repo should not mirror every agent, campaign, channel, client, or workflow as a separate skill.

## Core Principle

Each concept lives in one owner skill.

If another skill needs that concept, it should reference the owner instead of duplicating instructions. Duplication causes trigger conflicts, stale guidance, and context bloat.

## Preferred Skill Types

### Capability Skills

Durable behaviors used across many workflows.

Examples:

- Public output safety
- Brand voice
- Content strategy
- Research and source discipline
- Publishing operations
- CRM operations
- DAO operations

### Tool Operation Skills

Procedures for a specific API, CLI, app, or protocol where mistakes are costly or repetitive.

Examples:

- Portal CMS operations
- X API operations
- Discord send operations
- Bankr operations
- DAOhaus/Moloch operations

Tool operation skills should be narrow and safety-conscious. They should not own brand, content strategy, or public-output policy.

## Avoid As Skills

These usually belong as references, templates, or workflow notes inside a capability skill:

- Personas
- Campaigns
- Single channels
- One-off reports
- Client-specific variants
- Deprecated aliases
- Thin wrappers around another skill

## Progressive Disclosure

Use three layers:

1. `SKILL.md` frontmatter: concise trigger text.
2. `SKILL.md` body: essential workflow and routing.
3. `references/`: deeper rules, examples, rubrics, schemas, and channel-specific details.

Keep `SKILL.md` small enough that loading two to four skills together remains practical.

## Safety Baseline

Every public-facing workflow should route through the future public output safety skill before publication or presentation.

Public output safety should own:

- Secret scrubbing
- Client privacy checks
- Internal URL and local path checks
- Unsupported claim checks
- Debug/agent-language cleanup
- Persona/account mismatch detection

Other skills should reference that owner instead of repeating safety checklists.
