# Prism Skills Refactor Plan

This plan is based on the Prism skill and workflow reference export currently under `references/prism-skills/` and `references/prism-workflows/`.

## Diagnosis

The current Prism corpus is useful, but the skill boundaries are inconsistent:

- Some skills are durable capabilities, such as public output sanitization and RaidGuild voice.
- Some are live operation manuals, such as Portal CMS, Bankr, DAOhaus/Moloch, X API, Discord, and NextCRM.
- Some are persona or workflow wrappers, such as Queen Raida social output, Queen Raida campaign workflows, X activity reports, and draft queues.
- Some are aliases or narrow references that should not remain published skills.

The refactor should reduce trigger overlap by creating a smaller set of owner skills. Each owner skill should own one durable concept and move specific examples, personas, channel rules, and workflow recipes into on-demand references.

## Target Skill Set

### 1. `rg-public-output-safety`

Owns the final safety pass before public output is posted, queued, or presented for review.

Absorbs:

- `public-social-output-sanitizer`
- safety sections from `queen-raida-social-agent`
- safety sections from `rg-scribe-publisher-skill`
- relevant public-posting checks from `x-draft-queue`, `discord-send`, `bard-calendar-ops`, and public workflows

References to create:

- `references/secret-patterns.md`
- `references/public-claim-checks.md`
- `references/account-persona-mismatch.md`
- `references/output-json-contract.md`

Keep this skill strict and reusable. Other public-facing skills should call it instead of copying its checklist.

### 2. `rg-brand-voice`

Owns stable RaidGuild voice, AI Solutions voice, Queen Raida voice, and channel tone modulation.

Absorbs:

- `ai-solutions-brand-voice`
- voice doctrine and kill list from `rg-scribe-publisher-skill`
- voice/persona sections from `queen-raida-social-agent`
- voice/story-loop material from `queen-raida-dungeon-master-mode`

References to create:

- `references/raidguild-voice.md`
- `references/community-voice.md`
- `references/cultural-spice.md`
- `references/ai-solutions-voice.md`
- `references/queen-raida-voice.md`
- `references/language-anti-patterns.md`
- `references/channel-voice.md`

Do not put publishing mechanics, API details, or safety policy here. This skill should judge how something sounds and whether it fits the account or audience.

Build this skill from the layered corpus model in `docs/voice-corpus-plan.md`: institutional brand sources, origin stories, cultural spice sources, Prism Memory, and agent-persona repositories should feed separate references rather than one flattened voice guide.

### 3. `rg-content-strategy`

Owns campaign planning, editorial framing, content pillars, source-to-draft transformation, and draft quality evaluation.

Absorbs:

- strategy and adaptation sections from `rg-scribe-publisher-skill`
- content planning behavior from blog, brief, lore, field-notes, and Queen Raida workflows
- parts of `hivemind-consult` when used as a strategy input

References to create:

- `references/content-pillars.md`
- `references/editorial-rubric.md`
- `references/source-to-draft.md`
- `references/channel-formats.md`
- `references/workflow-patterns.md`

This skill should decide what to say, why it matters, and how to structure it. It should not publish, schedule, or operate APIs.

### 4. `rg-research`

Owns source discipline, current-event checks, source quality, claim verification, and research briefs.

Absorbs:

- `hn-news-scout`
- `hivemind-consult`
- research/source-discipline parts of `rg-scribe-publisher-skill`
- source-pack patterns from `field-notes-from-fireside`
- wiki/source research patterns from `fireside-wiki-topic-develop`

References to create:

- `references/source-quality.md`
- `references/claim-checking.md`
- `references/hacker-news-scouting.md`
- `references/hivemind-adapter.md`
- `references/research-brief-output.md`

Keep live API credentials and endpoint instructions in references or scripts, not in broad brand/content skills.

### 5. `rg-publishing-ops`

Owns publishing mechanics, approval gates, queues, calendars, channel sends, live URLs, and post-publication reconciliation.

Absorbs:

- `bard-calendar-ops`
- `discord-send`
- `x-draft-queue`
- publishing workflow pieces from Queen Raida, blog, brief, and weekly/daily workflows
- read/report parts of `raidguildish-x-activity-reporter`

References to create:

- `references/bard-calendar.md`
- `references/discord-send.md`
- `references/x-draft-queue.md`
- `references/publish-approval-gates.md`
- `references/live-url-reconciliation.md`

This skill should require `rg-public-output-safety` before any public post is queued or sent. It should not own voice or strategy.

### 6. `rg-portal-ops`

Owns Portal CMS and Payload API operations.

Absorbs:

- `portal-ops-skill`
- `portal-memory-publisher` as a deprecated alias
- Portal event/session artifact workflows
- Portal wiki/post/session update portions of workflows

References to create:

- `references/primitives.md`
- `references/events-and-discord-sync.md`
- `references/artifact-ingest.md`
- `references/wiki-pages.md`
- `references/posts-and-images.md`
- `references/page-copy.md`
- `references/confidence-and-review.md`

The current `portal-ops-skill` is too large for a single `SKILL.md`. Keep only operating rules, source inputs, routing, and safety in the main file; move endpoint-specific material into references.

Canonical app-specific source remains the Portal repo's in-repo skill package:

- `https://github.com/raid-guild/portal`
- `.agents/skills/portal-ops-skill/`

This repo should carry the portable distilled skill and cross-capability boundaries; use the Portal repo for current field schemas, endpoint drift, and app-local implementation details.

### 7. `rg-dao-ops`

Owns DAOhaus/Moloch governance, proposal watchers, share distro governance steps, and related read-only onchain evidence.

Absorbs:

- `moloch-dao-ops`
- `dao-proposal-watcher`
- `cookiejar-activity-reader`
- governance sections from `monthly-share-distro-proposal`

References to create:

- `references/moloch-agent.md`
- `references/proposal-watcher.md`
- `references/cookiejar-evidence.md`
- `references/share-distro-workflow.md`
- `references/approval-gates.md`

Keep a hard line between read-only evidence gathering, unsigned transaction building, and live transaction broadcast.

### 8. `rg-crm-ops`

Owns NextCRM MCP operations and CRM document/enrichment workflows.

Absorbs:

- `nextcrm`
- `crm-document-ingest-enrich`

References to create:

- `references/mcp-tools.md`
- `references/entities.md`
- `references/document-ingest.md`
- `references/privacy-rules.md`

This should stay separate because CRM data has different privacy and operational risks than public content.

Canonical app-specific source remains the Nexus CRM repo:

- `https://github.com/raid-guild/nexus-crm`
- MCP implementation under `lib/mcp/`
- route implementation under `app/api/mcp/[transport]/route.ts`

This repo should carry portable operator guidance, privacy boundaries, workflow handoffs, and cross-skill routing.

### 9. `rg-media-render-ops`

Owns Remotion render diagnostics, workflow audio upload, and media artifact preparation.

Absorbs:

- `remotion-composition-checker`
- `workflow-audio-bucket-uploader`
- media/render portions of podcast, recap video, and blog image workflows

References to create:

- `references/remotion-compositions.md`
- `references/audio-bucket.md`
- `references/render-payloads.md`
- `references/failure-recovery.md`

This is an ops skill, not a content skill. It should ensure render inputs are valid and fetchable.

### 10. `portal-arcade-reporter`

Keep as a standalone narrow read-only operations skill unless arcade reporting becomes part of a broader Portal analytics skill.

Reason:

- It has a clean API contract.
- It is read-only.
- Its trigger is distinct from CMS operations.

### 11. `rg-bankr-ops`

Keep as a standalone high-risk financial/tool operations skill.

Reason:

- Bankr has token launch, fee claim, wallet, and trading implications.
- Its approval gates should remain highly visible.
- It should not be buried inside generic DAO or publishing docs.

## Deprecated Or Reference-Only

These should not remain published standalone skills after migration:

- `portal-memory-publisher`: deprecated alias for Portal ops.
- `queen-raida-social-agent`: split into Queen Raida voice reference, content strategy pattern, publishing ops, and public safety.
- `queen-raida-dungeon-master-mode`: reference under Queen Raida voice or an optional story/gameplay reference, not a general-purpose skill.
- `rg-scribe-publisher-skill`: split into brand voice, content strategy, source discipline, and public output safety.
- `raidguildish-x-activity-reporter`: workflow/reference under publishing ops unless it needs a dedicated report script.
- `hn-news-scout`: reference under research unless it gains scripts/tooling.
- `hivemind-consult`: reference under research unless it needs robust API scripts.

## Migration Order

### Phase 1: Shared Policy And Voice

Create these first because many future skills should reference them:

1. `rg-public-output-safety`
2. `rg-brand-voice`
3. `rg-content-strategy`
4. `rg-research`

Validation task:

Use a Queen Raida X draft from workflow source material. The expected route is strategy draft, brand/voice pass, research/claim check when needed, then safety JSON.

### Phase 2: Publishing And Portal

Created:

1. `rg-publishing-ops`
2. `rg-portal-ops`

Validation task:

Use a workflow that drafts a Portal post, schedules or records a Bard Calendar event, produces Discord/X output, and reconciles live URLs after approval.

### Phase 3: High-Risk Operations

Created:

1. `rg-dao-ops`
2. `rg-bankr-ops`

Validation task:

Use read-only governance checks, build-only proposal payloads, Bankr prompt plans, and exact-parameter operator verification before live signing, broadcasting, token, wallet, or governance actions.

### Phase 4: Data And Media Ops

Created:

1. `rg-crm-ops`
2. `rg-media-render-ops`
3. `s3-object-storage`

Folded Portal Arcade API details into `rg-portal-ops/references/arcade-agent-apis.md` instead of creating a standalone `portal-arcade-reporter` skill. Recurring arcade reports should remain workflow recipes unless reporting becomes a broader durable capability.

Validation task:

Use read-only or dry-run tasks first: CRM entity lookup plan, Remotion schema inspection, audio URL validation, and arcade leaderboard reporting.

## Workflow Refactor Pattern

Do not turn each workflow into a skill. Treat workflows as recipes that compose skills.

For each workflow, extract:

- Inputs and source requirements
- Required skill sequence
- Approval gates
- Output artifacts
- Live-operation boundaries
- Public safety checkpoints

Then store the recipe as a reference under the closest owner skill, or keep it in `references/prism-workflows/` until a workflow runner format exists.

## Skill Template Guidance

Each new skill should start with this structure:

```text
skills/<skill-name>/
├── SKILL.md
└── references/
```

Main `SKILL.md` should include:

- what the skill owns
- what it does not own
- routing instructions to references
- approval and safety rules
- output expectations

Do not copy full legacy skills into `SKILL.md`. Extract the durable behavior and move detailed endpoints, examples, and long checklists into references.

## First Concrete Slice

The first implemented slice is:

```text
skills/rg-public-output-safety/
skills/rg-brand-voice/
skills/rg-content-strategy/
```

Use source material from:

- `references/prism-skills/public-social-output-sanitizer/SKILL.md`
- `references/prism-skills/rg-scribe-publisher-skill/SKILL.md`
- `references/prism-skills/ai-solutions-brand-voice/SKILL.md`
- `references/prism-skills/queen-raida-social-agent/SKILL.md`
- `references/prism-workflows/queen-raida-x-response-draft-review-publish/`
- `references/prism-workflows/blog-post-draft-review-publish/`
- `references/writing-anti-patterns.md`

Adopt the `cc-skills` style where useful: explicit BUILD / ADAPT / AUDIT modes, small `SKILL.md` routers, and deep anti-pattern inventories in references rather than in the main skill body.

This slice gives the repo immediate leverage because it removes the most duplicated policy, voice, and drafting behavior before touching risky live ops.

Next steps for this slice:

1. Enrich the references with reviewed examples from the voice corpus.
2. Forward-test realistic Queen Raida, AI Solutions, and public RaidGuild drafts.
3. Move repeated workflow-specific patterns into references instead of new skills.
