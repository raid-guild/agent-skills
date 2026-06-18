---
name: bard-calendar-ops
description: Use when Codex needs to inspect, create, upsert, patch, reconcile, or report on content publishing events in the Bard Calendar app, including workflow-generated content plans, chat-planned posts, publishing status updates, campaign metadata, owners, draft URLs, live URLs, and cross-channel content schedules.
---

# Bard Calendar Ops

Use Bard Calendar as the shared planning store for content publishing events.

## Auth

Require:

- `BARD_CALENDAR_BASE_URL`
- `BARD_CALENDAR_AGENT_API_TOKEN`

Send:

```text
Authorization: Bearer <BARD_CALENDAR_AGENT_API_TOKEN>
Content-Type: application/json
```

Do not expose the token in output, browser code, logs, or artifacts.

## Endpoints

Base URL is `BARD_CALENDAR_BASE_URL` with no required trailing slash.

### List Events

Use:

```http
GET /api/agent/events
```

Use this before updates when the target event id is not already known.

Common query filters:

- `start`
- `end`
- `status`
- `target_channel`
- `owner`
- `name`
- `search`

### Create Event

Use:

```http
POST /api/agent/events
```

Use for intentionally creating a new one-off event.

Required fields:

- `name`
- `publish_at`
- `target_channel`

### Upsert Event

Use:

```http
PUT /api/agent/events/upsert
```

Use for agent-generated or workflow-generated plans that may be regenerated.

Required identity fields:

- `external_source`
- `external_id`

Also include the normal event fields such as `name`, `publish_at`, and `target_channel`.

### Patch Event

Use:

```http
PATCH /api/agent/events/{id}
```

Use for updating existing calendar events by id. Send only changed fields. This is the default for status changes, metadata updates, adding draft URLs, adding live URLs, rescheduling, assigning owners, or updating human-created events.

## Event Fields

Common fields:

- `id`
- `name`
- `publish_at`
- `target_channel`
- `status`
- `content_type`
- `campaign`
- `owner`
- `draft_url`
- `media_url`
- `live_url`
- `notes`
- `metadata`
- `external_source`
- `external_id`
- `created_at`
- `updated_at`

Use ISO 8601 timestamps. Prefer UTC timestamps at the API boundary.

## Status Model

Use the app's returned status values when present. If choosing a status, prefer:

- `idea`
- `planned`
- `drafting`
- `ready`
- `scheduled`
- `published`
- `skipped`

For public post workflows, do not mark an event `published` unless the live URL or external evidence is known, or the user explicitly confirms publication.

## Decision Rules

- Use `GET /api/agent/events` for read/report tasks.
- Use `GET` before `PATCH` when the user describes an event but does not provide an id.
- Use `PATCH /api/agent/events/{id}` for existing events.
- Use `PUT /api/agent/events/upsert` for generated plans with stable `external_source` and `external_id`.
- Use `POST /api/agent/events` only when creating a genuinely new event.
- Preserve human-authored fields unless the user asks to overwrite them.
- Preview bulk writes before executing unless the user explicitly approved the operation.
- Avoid duplicate plans by searching the relevant date/channel/campaign before creating events.

## Metadata

Use `metadata` for source-agnostic planning state. Recommended keys:

- `workflow_id`
- `session_id`
- `source_request_id`
- `persona`
- `priority`
- `approval_state`
- `content_brief_url`
- `related_refs`
- `source_system`
- `source_version`

Do not put secrets, API tokens, private local paths, or internal-only operational notes in event metadata.

## Source Identity

For workflow-generated calendar entries, use stable source identity:

- `external_source`: short source label such as `prism-workflow`, `content-planning-chat`, `queen-raida-social-agent`, or `x-draft-queue`
- `external_id`: deterministic id derived from the source request, workflow step, campaign, channel, date, and content slug when available

Prefer stability over readability for `external_id`.

## Common Tasks

### Find Planned Content

1. List with date/channel/status filters.
2. Summarize by publish date, channel, status, campaign, and owner.
3. Call out missing draft URLs, missing owners, stale statuses, and overdue unpublished events when relevant.

### Add A Content Plan

1. Convert the plan into event objects.
2. Add `external_source` and `external_id` for workflow/chat-generated plans.
3. Use upsert for repeatable generated plans.
4. Use create for explicit one-off events.

### Update Status

1. Resolve the event id if needed.
2. Patch only `status` and any related fields.
3. For `published`, include `live_url` when known.

### Reconcile Plans

1. List the target date range and channels.
2. Match by `external_source + external_id` first.
3. Fall back to date/channel/name matching.
4. Patch existing events or upsert generated events.
5. Report skipped duplicates and ambiguous matches.

## Local Helper

When available, use `scripts/bard_calendar.mjs`:

```bash
node scripts/bard_calendar.mjs list --status planned
node scripts/bard_calendar.mjs create --json event.json
node scripts/bard_calendar.mjs upsert --json event.json
node scripts/bard_calendar.mjs patch --id <event-id> --json patch.json
```

The helper reads `BARD_CALENDAR_BASE_URL` and `BARD_CALENDAR_AGENT_API_TOKEN` from the environment and prints JSON.
