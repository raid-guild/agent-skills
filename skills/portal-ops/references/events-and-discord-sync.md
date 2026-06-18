# Events And Discord Sync

Use for Portal sessions/events and Discord scheduled event sync.

## Hard Rule

`syncDiscord` is not a field on the raw Payload `events` collection. Passing `"syncDiscord": true` to `POST /api/events` will be ignored and will not create a Discord scheduled event.

## Raw Payload Events

Use `POST /api/events` only for:

- Portal-only records
- imports
- past-session enrichment
- drafts
- records that already have external calendar/Discord links

## Portal Session Endpoint

When creating a future Portal session that should try to create a Discord scheduled event, use:

```http
POST /api/events/create
```

Use:

- `durationMinutes` instead of `endsAt`
- `hosts` instead of `hostProfiles`
- `guests` instead of `speakerProfiles`
- `syncDiscord: true` when the user asked for Discord sync

Do not send `_status` or `publishedAt`; the endpoint publishes the event.

## Existing Discord Event

If a Discord scheduled event already exists, send the Discord URL in `joinURL` or `discordEventURL`.

Portal recognizes:

```text
https://discord.com/events/<guildID>/<eventID>
```

and should link the event instead of creating a new one.

## Diagnostics

- `discordSyncStatus: synced` plus `discordEventURL`: Discord scheduled event exists.
- `discordSyncStatus: failed`: Portal event exists but Discord sync failed.
- `discordSyncStatus: not_configured`: request likely did not use `/api/events/create` with `syncDiscord: true`.

Do not tell users a Discord scheduled event was created unless the response has `discordSyncStatus: synced` and a `discordEventURL`.

## Recurring Sessions

Portal uses copied event metadata:

- `seriesKey`
- `seriesTitle`
- `recurrenceCadence`
- `recurrenceUntil`
- `previousOccurrence`
- `nextOccurrence`

When creating the next occurrence, copy series fields, set `previousOccurrence` on the new event, and patch `nextOccurrence` on the current event. Do not invent recurrence if the current event has no series fields.
