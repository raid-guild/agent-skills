# Apply Next Occurrence

Read `portal-session-artifact-ingest.json` and `portal-session-next-occurrence-plan.json`. Write exactly one final artifact: `portal-session-recording-complete-result.json`.

If plan action is `skip`, do not call Portal for recurrence. Write final status `success` if artifact ingest succeeded, otherwise `noop` or `failed` matching upstream status.

If plan action is `patch-existing`, authenticate to Portal, patch current event `nextOccurrence` only if missing, then write final result.

If plan action is `create`:

1. Re-fetch current event.
2. If `nextOccurrence` now exists, skip duplicate creation.
3. Search again for an event with `previousOccurrence` equal to current id.
4. If none exists, create exactly one next event from `createPayload`.
5. Patch current event `nextOccurrence` to the new/found event id.

Final result schema:

- `status`: `success`, `noop`, or `failed`.
- `matchedEventId`.
- `matchedBy`.
- `artifactIngest`.
- `artifactsAttached`.
- `nextOccurrence`: `created`, `skipped`, `patched-existing`, or `failed`.
- `nextOccurrenceId`.
- `reason`.
- `duplicatePreventionReason`.
- `errors`: concise array, no secrets.

Advance to `closed`.
