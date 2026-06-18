# Plan Next Occurrence

Read `portal-session-artifact-ingest.json`. Write exactly one artifact: `portal-session-next-occurrence-plan.json`. Do not write the final result artifact.

If ingest status is not `success`, write action `skip` with reason `artifact_ingest_not_successful` or the upstream reason.

If current event already has `nextOccurrence`, skip with duplicatePreventionReason `current_event_already_has_next_occurrence`.

If missing `seriesKey` or `recurrenceCadence`, skip with reason `not_recurring`.

Calculate next start/end:

- weekly: add 7 days.
- biweekly: add 14 days.
- monthly: add one calendar month and clamp invalid month days.

Respect `recurrenceUntil`: skip if next start is after it.

Before planning creation, search Portal for an existing event whose `previousOccurrence` equals the current event id. If found, action is `patch-existing`.

Schema:

- `action`: `create`, `patch-existing`, or `skip`.
- `reason` and/or `duplicatePreventionReason`.
- `currentEventId`.
- `existingNextOccurrenceId` when found.
- `nextStart` / `nextEnd` when create.
- `createPayload` with only copied real Portal fields allowed by the original request.
- `errors`: concise array, no secrets.
