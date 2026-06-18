# Agent Instructions

This repo contains reusable RaidGuild agent skills. Treat it as a maintainability project first and a skill-writing project second.

## Working Rules

- Do not create a new skill for a one-off campaign, persona, client, channel, or workflow.
- Create a new skill only when it owns a durable capability that will be reused across tasks.
- Put raw source material under `references/prism-skills/raw/`.
- Put analysis, inventories, and migration notes under `references/prism-skills/`.
- Keep `skills/` empty until a candidate skill has a clear boundary, migration source, and validation path.
- Do not commit secrets, tokens, internal URLs, client-private details, wallet keys, private operational notes, or environment-specific paths.
- Prefer concise `SKILL.md` files with deeper material in local `references/` files.
- Use cross-references instead of copying rules between skills.

## Skill Boundary Test

Before adding a skill, answer:

1. What durable capability does this skill own?
2. Which existing Prism skills does it absorb or supersede?
3. Which rules belong in shared safety, brand, research, or publishing skills instead?
4. What references should be loaded only on demand?
5. How will the skill be validated on a realistic task?

If those answers are unclear, keep the work in `references/prism-skills/` until the boundary is clearer.

## File Policy

- `skills/`: only published skills.
- `references/prism-skills/raw/`: unmodified exports or copied source material from Prism.
- `references/prism-skills/inventory.md`: structured list of current Prism skills and migration decisions.
- `references/prism-skills/refactor-notes.md`: observations, grouping ideas, and open questions.
- `docs/`: repo-level architecture and process docs.
