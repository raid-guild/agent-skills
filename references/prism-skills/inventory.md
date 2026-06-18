# Prism Skills Inventory

Use this file to track current Prism skills and their migration target.

| Current Skill | Primary Behavior | Dependencies | Safety Concerns | Proposed Owner | Decision | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| ai-solutions-brand-voice | Buyer-facing AI Solutions copy and voice checks | Unknown | Public claims, brand consistency | rg-brand-voice | reference | Move into `references/ai-solutions-voice.md`. |
| bankr-ops | Bankr CLI planning and reviewed operations | Bankr CLI, wallet context | Financial actions, token launches, fees, wallets | rg-bankr-ops | keep | Migrated to `skills/rg-bankr-ops` with operator-verification framing. |
| bard-calendar-ops | Content publishing calendar records | Bard Calendar app | Publishing status accuracy, draft/live URLs | rg-publishing-ops | merge | Migrated to `skills/rg-publishing-ops/references/bard-calendar.md`. |
| cookiejar-activity-reader | CookieJar V3 onchain withdrawal evidence | Onchain read APIs | Financial/onchain interpretation | rg-dao-ops | merge | Migrated to `skills/rg-dao-ops/references/cookiejar-evidence.md`. |
| dao-proposal-watcher | DAOhaus/Moloch proposal watcher | DAOhaus/Moloch APIs, scheduler | Governance accuracy, notifications | rg-dao-ops | merge | Migrated to `skills/rg-dao-ops/references/proposal-watcher.md`. |
| discord-send | Approved Discord send workflow | Communication adapter | Wrong destination, unapproved posting | rg-publishing-ops | merge | Migrated to `skills/rg-publishing-ops/references/discord-send.md`. |
| hivemind-consult | Hivemind marketing copilot/API context | Hivemind API key | Source quality, private context | rg-research | reference | Research adapter unless robust scripts are added. |
| hn-news-scout | HN scanning for post angles | Hacker News | Relevance, current claims | rg-research | reference | Research scouting workflow. |
| moloch-dao-ops | DAOhaus/Moloch inspect/propose/vote/process | meta-clawtel, moloch-agent | Governance transactions | rg-dao-ops | merge | Migrated to `skills/rg-dao-ops/references/moloch-agent.md`. |
| nextcrm | CRM MCP operations | Nexus CRM / NextCRM MCP | Client/customer data privacy | rg-crm-ops | keep | Migrated to `skills/rg-crm-ops`; canonical implementation remains `https://github.com/raid-guild/nexus-crm`. |
| portal-arcade-reporter | Portal Arcade read-only reporting | Game reporting APIs | Public/private leaderboard context | rg-portal-ops / workflow recipes | reference | API contract migrated to `skills/rg-portal-ops/references/arcade-agent-apis.md`; recurring reports stay workflows. |
| portal-memory-publisher | Deprecated alias for portal ops | Portal APIs | Alias drift | rg-portal-ops | deprecate | Replaced by `skills/rg-portal-ops`. |
| portal-ops-skill | Portal CMS operations | Payload API | Invented content, project-management drift | rg-portal-ops | keep | Migrated to `skills/rg-portal-ops` with endpoint details split into references. |
| public-social-output-sanitizer | Public output sanitization | None or text-only | Secrets, private info, unsupported claims | rg-public-output-safety | merge | Strong candidate first skill. |
| queen-raida-dungeon-master-mode | Queen Raida story loop testing | Chat/Discord context | Persona drift | rg-brand-voice | reference | Persona/gameplay reference, not standalone. |
| queen-raida-social-agent | Queen Raida X/social drafting/posting | Prism, Portal, X | Public posting, account voice, factual grounding | rg-brand-voice / rg-publishing-ops | reference | Split persona from publishing mechanics. |
| raidguildish-x-activity-reporter | X activity reports into Prism Memory | X data, Prism Memory | Public/social analytics accuracy | rg-publishing-ops | reference | Reporting workflow reference unless scripts are needed. |
| remotion-composition-checker | Remotion renderer inspection | Remotion renderer | Render diagnostics | rg-media-render-ops | merge | Migrated to `skills/rg-media-render-ops/references/remotion-compositions.md`. |
| rg-scribe-publisher-skill | RaidGuild public copy drafting | Source context | Voice, unsupported claims, public safety | rg-content-strategy / rg-brand-voice | merge | Split into strategy, voice, and safety. |
| workflow-audio-bucket-uploader | Upload audio to S3-compatible bucket | S3-compatible storage | Public URLs, credentials | s3-object-storage / rg-media-render-ops | merge | Generic storage migrated to `s3-object-storage`; Remotion-specific audio input rules migrated to `rg-media-render-ops`. |
| x-developer-api | X API development and operations | X Developer API | Posting, DMs, rate limits | rg-publishing-ops | merge | Migrated as lightweight routing reference; split later if API detail grows. |
| x-draft-queue | Autonomous X draft queue | X queue system | Autonomous posting | rg-publishing-ops | merge | Migrated to `skills/rg-publishing-ops/references/x-draft-queue.md`. |

## Decision Legend

- `keep`: remains a standalone skill
- `merge`: absorbed into a capability skill
- `reference`: becomes a reference file, template, persona profile, or workflow note
- `deprecate`: remove after replacement exists
- `unknown`: needs review
