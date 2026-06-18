# Prism Skill Reference Export

This directory contains reference copies of the current Prism custom skills exported on 2026-06-18.

These files are source material for the RaidGuild skill migration. They are not published repo skills yet, and `skills/` should remain empty until a candidate skill has a clear durable boundary, migration source, and validation path.

## Source

- Source service: Prism site service skill API
- List endpoint: `GET /agent/skills`
- Download endpoint pattern: `GET /agent/skills/<skill-name>/download`
- Auth used for export: service-token auth from the agent runtime environment

Built-in and system skills are intentionally excluded. Only skills returned by the service as custom skills were exported.

Instance-local filesystem paths from the live runtime are normalized to `<instance-custom-data>` when needed to keep this repository free of environment-specific paths.

## Exported Skills

| Skill | Source kind | Reference copy |
| --- | --- | --- |
| ai-solutions-brand-voice | custom | references/prism-skills/ai-solutions-brand-voice/SKILL.md |
| bankr-ops | custom | references/prism-skills/bankr-ops/SKILL.md |
| bard-calendar-ops | custom | references/prism-skills/bard-calendar-ops/SKILL.md |
| cookiejar-activity-reader | custom | references/prism-skills/cookiejar-activity-reader/SKILL.md |
| dao-proposal-watcher | custom | references/prism-skills/dao-proposal-watcher/SKILL.md |
| discord-send | custom | references/prism-skills/discord-send/SKILL.md |
| hivemind-consult | custom | references/prism-skills/hivemind-consult/SKILL.md |
| hn-news-scout | custom | references/prism-skills/hn-news-scout/SKILL.md |
| moloch-dao-ops | custom | references/prism-skills/moloch-dao-ops/SKILL.md |
| nextcrm | custom | references/prism-skills/nextcrm/SKILL.md |
| portal-arcade-reporter | custom | references/prism-skills/portal-arcade-reporter/SKILL.md |
| portal-memory-publisher | custom | references/prism-skills/portal-memory-publisher/SKILL.md |
| portal-ops-skill | custom | references/prism-skills/portal-ops-skill/SKILL.md |
| public-social-output-sanitizer | custom | references/prism-skills/public-social-output-sanitizer/SKILL.md |
| queen-raida-dungeon-master-mode | custom | references/prism-skills/queen-raida-dungeon-master-mode/SKILL.md |
| queen-raida-social-agent | custom | references/prism-skills/queen-raida-social-agent/SKILL.md |
| raidguildish-x-activity-reporter | custom | references/prism-skills/raidguildish-x-activity-reporter/SKILL.md |
| remotion-composition-checker | custom | references/prism-skills/remotion-composition-checker/SKILL.md |
| rg-scribe-publisher-skill | custom | references/prism-skills/rg-scribe-publisher-skill/SKILL.md |
| workflow-audio-bucket-uploader | custom | references/prism-skills/workflow-audio-bucket-uploader/SKILL.md |
| x-developer-api | custom | references/prism-skills/x-developer-api/SKILL.md |
| x-draft-queue | custom | references/prism-skills/x-draft-queue/SKILL.md |

## Refresh Process

1. Query `GET /agent/skills` with `x-service-token` service auth.
2. Filter to custom skills only.
3. Download each custom skill archive from its `downloadPath`.
4. Copy each archive's `<skill-name>/SKILL.md` to `references/prism-skills/<skill-name>/SKILL.md`.
5. Normalize instance-local filesystem paths to `<instance-custom-data>` if present.
6. Update this index with the new export date and exported skill list.
7. Review the diff for secrets, private client context, runtime artifacts, generated outputs, and accidental built-in/system skill exports.
