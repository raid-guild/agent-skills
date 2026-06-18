# Intake

Use `rg-portal-ops`.

Read the recording completion event, Portal session/event id, Discord thread/channel context, recording URL, transcript URL, summary URL, and any attached artifact metadata.

Produce `portal-recording-intake.md` with:

- Portal session/event id and URL
- recording, transcript, summary, and artifact URLs
- source event id or webhook reference
- missing required fields
- whether recurrence rules appear relevant

Do not infer the target session if the event cannot be matched confidently.
