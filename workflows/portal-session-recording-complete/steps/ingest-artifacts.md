# Ingest Artifacts

Use `rg-portal-ops`.

Attach the recording, transcript, summary, and related artifacts to the matched Portal session/event resources.

Preserve existing resources. Avoid duplicates by URL and label. Re-read the Portal record after writing and verify the expected resources are present.

Produce `portal-recording-ingest-verification.json` with event id, updated resource list, created/updated fields, skipped artifacts, and failures.
