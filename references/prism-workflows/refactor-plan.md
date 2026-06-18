# Prism Workflow Refactor Plan

The skill refactor reduced the published skill surface. Workflows should now be deduplicated and rewritten to compose durable capabilities instead of legacy one-off skills.

## New Skill Sequence Vocabulary

Use these skill names in refactored workflow manifests and step instructions:

- `rg-content-strategy`
- `rg-brand-voice`
- `rg-public-output-safety`
- `rg-publishing-ops`
- `rg-portal-ops`
- `rg-dao-ops`
- `rg-bankr-ops`
- `s3-object-storage`
- `rg-media-render-ops`
- `rg-crm-ops`
- `rg-research`

External built-in capability surfaced by workflow analysis:

- none currently. Prism Memory and target deploy behavior are covered by Prism built-in skills; see `docs/prism-builtin-skills.md`.

## Legacy Skill Mapping

| Legacy workflow skill | New capability |
| --- | --- |
| `rg-scribe-publisher-skill` | `rg-content-strategy` + `rg-brand-voice` |
| `ai-solutions-brand-voice` | `rg-brand-voice` |
| `queen-raida-social-agent` | `rg-brand-voice` + `rg-content-strategy` |
| `public-social-output-sanitizer` | `rg-public-output-safety` |
| `bard-calendar-ops` | `rg-publishing-ops` |
| `discord-send` | `rg-publishing-ops` |
| `x-developer-api` | `rg-publishing-ops` |
| `x-draft-queue` | `rg-publishing-ops` |
| `portal-memory-publisher` | `rg-portal-ops` |
| `portal-ops-skill` | `rg-portal-ops` |
| `moloch-dao-ops` | `rg-dao-ops` |
| `cookiejar-activity-reader` | `rg-dao-ops` |
| `dao-proposal-watcher` | `rg-dao-ops` |
| `workflow-audio-bucket-uploader` | `s3-object-storage` + `rg-media-render-ops` |
| `remotion-composition-checker` | `rg-media-render-ops` |
| `nextcrm` | `rg-crm-ops` |
| `portal-arcade-reporter` | `rg-portal-ops` reference + reporting workflow |

## Prism Built-In Dependencies

Do not recreate these as RaidGuild portable skills:

- Prism Memory built-ins from `services/prism-memory/skills`: `prism-api-reader`, `prism-api-writer`, `prism-api-ops`, `prism-config-admin`, `prism-discord-promote-doc`, `prism-knowledge-sources`.
- Prism Site built-ins from `services/site/skills`: `change-request-ops`, `target-deploy-ops`, `prism-workflow-author`, `prism-skill-author`, `prism-task-author`, `prism-scheduled-task-runner`, `prism-instance-profile`, `prism-instance-settings`, `prism-hook-author`.

Use these as runtime dependencies when importing recipes into Prism.

## Refactor Process

1. Keep exported workflows immutable as reference copies.
2. Create new normalized workflow recipes instead of editing reference exports directly.
3. For duplicate families, keep the highest-version workflow as the base unless a lower-version workflow has the better canonical structure.
4. Move repeated instructions into skill references only when they are durable capability guidance.
5. Keep campaign-specific sequencing as workflow references.
6. Run one realistic forward test per canonical family.

## Node Semantics

Workflow recipes should use three node types:

- `agent`: Codex/agent work node.
- `gate`: human gate for steering, review, approval, rejection, or pause.
- `checkpoint`: long-running or indeterminate external job checkpoint.

Execution behavior:

- A workflow whose first node is a human `gate` always waits for human input before agent work starts.
- `autoRun: true` on an `agent` node means the agent step may continue automatically when reached.
- `autoRun: false` on an `agent` node means the workflow waits for an operator to continue/start that agent step.
- Human `gate` nodes always wait, regardless of `autoRun`.
- `checkpoint` nodes wait for external job state, webhook/event reconciliation, or operator confirmation before routing onward.

Use first-node human gates for workflows that need steering before the agent should infer scope, such as open-ended blog posts or campaign briefs.

Use `autoRun: false` on child requests spawned by parent workflows when a human should review the spawned request before it begins. This is the pattern used by Field Notes From Fireside when it creates follow-on blog, wiki, and recap video requests.

## Canonical Workflow Families

### Blog / Editorial Publish

Base candidate: `blog-post-steered-draft-review-publish`.

Merge in generic blog, fireside blog, and lore entry modes.

Normalized sequence: intake/source ledger -> `rg-content-strategy` -> draft -> `rg-brand-voice` -> media if needed -> `rg-public-output-safety` -> human review -> `rg-portal-ops`.

Implemented recipe:

- `workflows/blog-editorial-publish/`

### Field Notes From Fireside

Base candidate: `field-notes-from-fireside` v17.

Keep as orchestration parent. It should produce source packs and spawn or queue child recipes rather than duplicating blog/wiki/video publish logic.

Implemented recipe:

- `workflows/field-notes-from-fireside/`

### Brief / Podcast / Media

Base candidate: `weekly-public-brief-podcast-publish` v9.

Variants: public weekly brief, internal/member daily brief, fireside recap video, brief without media.

Normalized media sequence: source intake -> strategy -> script/summary -> voice/safety where public -> TTS artifacts -> `s3-object-storage` -> `rg-media-render-ops` -> review -> `rg-portal-ops`.

Implemented recipe:

- `workflows/brief-media-publish/`

### Queen Raida Social

Base candidate: `queen-raida-x-response-draft-review-publish` v5.

Merge in launch campaign as a campaign wrapper. Keep follow scout under review because follow actions are social graph/account operations rather than publishing.

Implemented recipe:

- `workflows/queen-raida-social-publish/`

### DAO Share Distro

Base candidate: `monthly-share-distro-proposal` v6.

Keep canonical. Use `rg-dao-ops` for evidence, build-only payloads, operator verification, and submission; use `rg-publishing-ops` for Discord review output.

Implemented recipe:

- `workflows/dao-share-distro-proposal/`

### CRM Document Ingest

Base candidate: `crm-document-ingest-enrich` v3.

Keep canonical and narrow. Use `rg-crm-ops`.

Implemented recipe:

- `workflows/crm-document-ingest/`

### Portal Session Recording Complete

Base candidate: `portal-session-recording-complete` v4.

Keep canonical. Use `rg-portal-ops` artifact ingest and recurrence rules.

Implemented recipe:

- `workflows/portal-session-recording-complete/`

### Portal Activity / Arcade Reporting

Base candidate: `weekly-portal-activity-snapshot`.

Keep as workflow-reference. Fold Portal Arcade reporting recipes here or in a sibling reporting workflow. Do not create `portal-arcade-reporter` as a standalone skill unless reporting becomes a broader durable capability.

Implemented recipe:

- `workflows/portal-activity-report/`

### Wiki / Research

Base candidate: `fireside-wiki-topic-develop` v4.

Keep canonical. Use `rg-research`, `rg-content-strategy`, `rg-brand-voice`, `rg-public-output-safety`, and `rg-portal-ops`.

Implemented recipe:

- `workflows/fireside-wiki-topic-develop/`

### Memory Ingest

Base candidate: `meeting-transcript-memory-ingest` v1.

Keep as a narrow workflow-reference. It depends on Prism built-ins `prism-api-writer` and `change-request-ops`.

Implemented recipe:

- `workflows/meeting-transcript-memory-ingest/`

### Queen Raida Social Graph

Base candidate: `queen-raida-x-follow-scout-review-follow` v1.

Keep separate from publishing because follow actions change account graph, not content.

Implemented recipe:

- `workflows/queen-raida-social-graph-ops/`

### Queen Raida Article Publish

Base candidate: `publish-queen-raida-article` v1.

Keep as a repo-target workflow-reference. It depends on Prism built-in `target-deploy-ops`.

Implemented recipe:

- `workflows/queen-raida-article-publish/`

## Immediate Next Steps

1. Forward-test the normalized workflow recipes with realistic source packages.
2. Convert accepted recipes into whatever Prism runtime import format is required.
3. Use Prism built-ins for request/memory/deploy/import behavior instead of duplicating those contracts in this repo.
4. Leave source exports untouched for auditability.
