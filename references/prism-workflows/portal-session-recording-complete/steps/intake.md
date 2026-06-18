# Intake

Read `hook-payload.json`. Normalize identifiers and artifact references. Do not call Portal. Do not write the final result artifact.

Write exactly one artifact: `portal-session-intake.json`.

Schema:

- `status`: `continue` or `noop`.
- `reason`: `missing_event_identifier` when status is noop.
- `matchedBy`: `eventID`, `discordScheduledEventID`, or null.
- `eventID`: normalized event id or null.
- `discordScheduledEventID`: normalized Discord scheduled event id or null.
- `artifacts`: object with present values only: `recordingUrl`, `transcriptUrl`, `summaryUrl`, `sourceArtifactID`.
- `receivedAt` when available.

Identifier precedence:

1. `eventID` / `eventId`.
2. `discord.scheduledEventID`, `discord.scheduledEventId`, `scheduledEventID`, `scheduledEventId`.

Artifact aliases:

- recording: top-level `recordingUrl`, `recordingURL`, nested `recording.url`, `artifacts.recordingUrl`, `artifacts.recording.url`.
- transcript: equivalent transcript fields.
- summary: equivalent summary fields.
- source artifact: `sourceArtifactID`, `sourceArtifactId`, `artifactId`, `sourceArtifact.id`, `artifacts.sourceArtifactID`, `artifacts.sourceArtifactId`.
