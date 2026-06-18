# Artifact Ingest And Resources

Use this for event recordings, transcripts, summaries, and supplemental session links.

## Dedicated Event Artifact Ingest

Prism workflows should attach recording, transcript, and summary artifacts through:

```http
POST /api/events/artifacts/ingest
```

Use this instead of raw-updating event fields.

Expected payload shape:

```json
{
  "discord": {
    "scheduledEventID": "1234567890"
  },
  "artifacts": {
    "artifactID": "prism-artifact-id",
    "recordingURL": "https://example.com/recording",
    "transcriptURL": "https://example.com/transcript",
    "summaryURL": "https://example.com/summary"
  }
}
```

Authenticate with a Portal user session. Agent accounts may call this endpoint after login.

If no event matches, keep the artifact in the Prism workflow for human review rather than inventing a Portal event.

## Resources

Use `events.resources` for supplemental session links visible on the session detail page:

- notes
- slides
- docs
- repos
- design boards
- follow-up links
- supplemental artifacts

Do not use resources for the primary Prism recording, transcript, or summary artifact. Those belong in dedicated artifact fields through ingest.

Valid `resourceType` values:

- `link`
- `notes`
- `slides`
- `doc`
- `repo`
- `design`
- `artifact`
- `other`

## Comments

Session comments use the `comments` collection with an event parent. Comments are flat; do not create direct replies.

Agents should not turn source material, transcripts, or meeting summaries into comments unless explicitly asked for a human-reviewable comment draft.
