# Prism Skills Inventory

Use this file to track current Prism skills and their migration target.

| Current Skill | Primary Behavior | Dependencies | Safety Concerns | Proposed Owner | Decision | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| ai-solutions-brand-voice | Buyer-facing AI Solutions copy and voice checks | Unknown | Public claims, brand consistency | rg-brand-voice | unknown | Likely reference under brand voice. |
| bankr-ops | Bankr CLI planning and reviewed operations | Bankr CLI, wallet context | Financial actions, token launches, fees, wallets | rg-bankr-ops | unknown | Keep narrow with explicit approval gates. |
| bard-calendar-ops | Content publishing calendar records | Bard Calendar app | Publishing status accuracy, draft/live URLs | rg-publishing-ops | unknown | Likely reference or tool-operation section. |
| cookiejar-activity-reader | CookieJar V3 onchain withdrawal evidence | Onchain read APIs | Financial/onchain interpretation | unknown | unknown | Review for DAO/share distro grouping. |
| dao-proposal-watcher | DAOhaus/Moloch proposal watcher | DAOhaus/Moloch APIs, scheduler | Governance accuracy, notifications | rg-dao-ops | unknown | Could be reference or script under DAO ops. |
| discord-send | Approved Discord send workflow | Communication adapter | Wrong destination, unapproved posting | rg-publishing-ops | unknown | Publishing op with approval gate. |
| hivemind-consult | Hivemind marketing copilot/API context | Hivemind API key | Source quality, private context | rg-research | unknown | Likely research source adapter. |
| hn-news-scout | HN scanning for post angles | Hacker News | Relevance, current claims | rg-research | unknown | Likely research reference/workflow. |
| moloch-dao-ops | DAOhaus/Moloch inspect/propose/vote/process | meta-clawtel, moloch-agent | Governance transactions | rg-dao-ops | unknown | Keep as narrow ops skill. |
| nextcrm | CRM MCP operations | NextCRM MCP | Client/customer data privacy | rg-crm-ops | unknown | Keep as narrow ops skill. |
| portal-arcade-reporter | Portal Arcade read-only reporting | Game reporting APIs | Public/private leaderboard context | unknown | unknown | Maybe Portal reporting ops. |
| portal-memory-publisher | Deprecated alias for portal ops | Portal APIs | Alias drift | portal-ops | deprecate | Replace with canonical owner. |
| portal-ops-skill | Portal CMS operations | Payload API | Invented content, project-management drift | portal-ops | unknown | Keep as canonical tool op. |
| public-social-output-sanitizer | Public output sanitization | None or text-only | Secrets, private info, unsupported claims | rg-public-output-safety | merge | Strong candidate first skill. |
| queen-raida-dungeon-master-mode | Queen Raida story loop testing | Chat/Discord context | Persona drift | rg-brand-voice | reference | Likely persona/workflow reference, not standalone. |
| queen-raida-social-agent | Queen Raida X/social drafting/posting | Prism, Portal, X | Public posting, account voice, factual grounding | rg-brand-voice / rg-publishing-ops | reference | Split persona from publishing mechanics. |
| raidguildish-x-activity-reporter | X activity reports into Prism Memory | X data, Prism Memory | Public/social analytics accuracy | rg-publishing-ops | unknown | Maybe reporting workflow reference. |
| remotion-composition-checker | Remotion renderer inspection | Remotion renderer | Render diagnostics | unknown | unknown | Probably tool op if still active. |
| rg-scribe-publisher-skill | RaidGuild public copy drafting | Source context | Voice, unsupported claims, public safety | rg-content-strategy / rg-brand-voice | merge | Split into strategy, voice, and safety. |
| workflow-audio-bucket-uploader | Upload audio to S3-compatible bucket | S3-compatible storage | Public URLs, credentials | unknown | unknown | Tool op if still active. |
| x-developer-api | X API development and operations | X Developer API | Posting, DMs, rate limits | rg-publishing-ops | unknown | Possibly narrow X API tool reference. |
| x-draft-queue | Autonomous X draft queue | X queue system | Autonomous posting | rg-publishing-ops | unknown | Keep as publishing workflow reference. |

## Decision Legend

- `keep`: remains a standalone skill
- `merge`: absorbed into a capability skill
- `reference`: becomes a reference file, template, persona profile, or workflow note
- `deprecate`: remove after replacement exists
- `unknown`: needs review
