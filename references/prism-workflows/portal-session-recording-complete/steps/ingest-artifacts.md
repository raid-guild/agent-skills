# Ingest Artifacts

Read `portal-session-intake.json`. Write exactly one artifact: `portal-session-artifact-ingest.json`. Do not write the final result artifact.

If intake status is not `continue`, write:

- `status: "noop"`
- `reason` from intake.
- `artifactIngest: "skipped"`
- `portalEvent: null`

and do not call Portal.

When intake can continue:

1. Authenticate to Portal using `PAYLOAD_CMS_BASE_URL`, `PAYLOAD_CMS_EMAIL`, and `PAYLOAD_CMS_PASSWORD`. Do not log/store secrets, auth tokens, or cookies.
2. Call `POST /api/events/artifacts/ingest` using the reliable identifier and only available artifact fields.
3. Treat the response as the matched event if it returns a document. Otherwise fetch the event by id or query by Discord scheduled event id.
4. If no event is found, write status `noop`, reason `portal_event_not_found`.

Artifact schema:

- `status`: `success`, `noop`, or `failed`.
- `reason` when applicable.
- `matchedEventId`.
- `matchedBy`.
- `artifactIngest`: `success`, `skipped`, or `failed`.
- `artifactsAttached`: booleans for recordingUrl, transcriptUrl, summaryUrl, sourceArtifactID.
- `portalEvent`: event snapshot sufficient for recurrence planning, or null.
- `errors`: concise array, no secrets.
