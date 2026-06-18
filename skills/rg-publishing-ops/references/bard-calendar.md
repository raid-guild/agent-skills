# Bard Calendar

Use Bard Calendar as the shared planning store for content publishing events.

## Environment

Require:

- `BARD_CALENDAR_BASE_URL`
- `BARD_CALENDAR_AGENT_API_TOKEN`

Send:

```text
Authorization: Bearer <BARD_CALENDAR_AGENT_API_TOKEN>
Content-Type: application/json
```

Do not expose the token in output, logs, browser code, or artifacts.

## Endpoints

- `GET /api/agent/events`: list or search events.
- `POST /api/agent/events`: create an intentional one-off event.
- `PUT /api/agent/events/upsert`: upsert generated plans with stable identity.
- `PATCH /api/agent/events/{id}`: update known event fields.

## Common Fields

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

Use ISO 8601 timestamps. Prefer UTC at the API boundary.

## Status Values

Prefer app-returned values. If choosing:

- `idea`
- `planned`
- `drafting`
- `ready`
- `scheduled`
- `published`
- `skipped`

Do not mark `published` unless live URL or external evidence is known, or the user explicitly confirms publication.

## Decision Rules

- Use `GET` before `PATCH` when the id is unknown.
- Use `PATCH` for existing events.
- Use `upsert` for repeatable workflow/chat-generated plans with stable `external_source` and `external_id`.
- Use `POST` only for genuinely new one-off events.
- Preserve human-authored fields unless the user asks to overwrite them.
- Preview bulk writes before executing unless approved.
- Search date/channel/campaign before creating events to avoid duplicates.

## Metadata

Good metadata keys:

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

Do not put secrets, tokens, private local paths, or internal-only operational notes in metadata.
