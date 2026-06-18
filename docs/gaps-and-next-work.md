# Gaps And Next Work

This repo now has portable RaidGuild capability skills and normalized workflow recipes. The remaining gaps are mostly runtime integration, validation, and corpus depth.

## 1. Prism Runtime Import Format

The workflow recipes under `workflows/` use normalized `manifest.proposal.json` files and markdown step instructions.

Next work:

- confirm the exact Prism workflow import/registration shape
- convert accepted recipes to that runtime format
- use Prism built-in `prism-workflow-author` when operating inside Prism
- keep `references/prism-workflows/` as immutable source exports

## 2. Forward Tests

The recipes validate structurally, but need realistic runs before treating them as production-ready.

Test candidates:

- Queen Raida X response/campaign source package
- Portal session recording/event artifact package
- weekly public brief or internal daily brief
- DAO share distro cycle
- CRM document handoff event
- Fireside source pack spawning blog/wiki/media child requests

## 3. X API Runtime Access

The X API skill surface already exists.

Current mapping:

- legacy reference: `references/prism-skills/x-developer-api/SKILL.md`
- durable capability: `skills/rg-publishing-ops`
- workflow users: `queen-raida-social-publish`, `queen-raida-social-graph-ops`, and publishing/reporting recipes

The remaining gap is not skill design. The remaining question is whether the active runtime has approved credentials and permissions for the requested X account/action.

Use X only when the operator has approved the exact account, action, destination, and final text/handle set.

## 4. Official Social Voice Corpus

`@RaidGuild` is now identified as the official HQ public-social voice source, separate from Queen Raida's `@raidguildish` persona.

Next work:

- collect 20-50 high-signal `@RaidGuild` public posts through X API, approved export, or another approved source
- extract cadence, wording, CTA style, topic boundaries, and account posture
- update `skills/rg-brand-voice/references/raidguild-core-voice.md` and `channel-voice.md`

## 5. Voice Corpus Second Pass

The first extraction pass added community voice, cultural spice, stronger Queen Raida boundaries, channel modulation, and anti-pattern replacements.

Useful next pass:

- deeper handbook glossary/role extraction
- Queen Raida site article patterns
- current Railway Prism Memory examples, not only local March snapshots
- more public-safe examples from Portal posts and official RaidGuild social

Keep extracted references compact. Do not turn source repos or memory dumps into skill context.

## 6. Validation Tooling

Current validation:

- all workflow manifests pass `jq`
- skill structure has been manually checked

Missing repo-local validation:

- `SKILL.md` frontmatter validation
- broken reference-link checks
- workflow manifest dependency checks
- distinction between repo skills and Prism built-in skills
- unknown step instruction path checks

This could be a small script under `scripts/` if repeated often.

## 7. Source Adapter Scripts

`rg-research` documents HN, Hivemind, source ledgers, claim confidence, and DuckDuckGo/ddgs fallback behavior.

Scripts are not required yet. Add scripts only if repeated tasks need deterministic output:

- HN scouting/ranking
- Hivemind query wrapper
- source ledger normalization

## 8. Built-In Skill Boundaries

Do not recreate Prism service built-ins as RaidGuild portable skills.

Reference:

- `docs/prism-builtin-skills.md`

Use built-ins for Prism Memory, change requests, workflow authoring, target deploys, scheduled tasks, and instance settings.
