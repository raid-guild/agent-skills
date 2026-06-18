# Build Cycle Distro

Turn the Participation Steward cycle evidence into a share distro proposal dataset.

## Inputs

Use the artifacts from Collect Cycle Activity plus the primary Participation Steward cycle artifact. For AprMay2026, the expected exported artifact is `docs/participation-steward/aprmay2026.md`.

## Current scoring model

Use the Participation Steward cycle matrix unless the request explicitly asks for a historical monthly rerun:

- Engagement: 20
- Stewardship: 60
- Contribution: 70
- Maximum cycle gain: 150

Do not use the old monthly HallMonitor weights:

- Raid: 40
- RIP: 40
- CookieJar: 10
- Meeting: 10

CookieJar is optional/historical evidence only and should not create a score by itself unless the reviewed cycle artifact explicitly says so.

## Required artifacts

Write:

- `share-distro.md`
- `share-distro.json`

The JSON should make scoring auditable per member, including:

- member display name
- discord handle if known
- wallet
- cycle key
- cycle start and end dates
- engagement score and evidence
- stewardship score and evidence
- contribution score and evidence
- total cycle gains
- prior shares, when present in the source artifact
- resulting total, when present in the source artifact
- notes
- audit flags or unresolved evidence

The markdown artifact should include a readable per-member breakdown so a later Discord report can explain how each person got shares without recomputing the distro from scratch.

## Review posture

When the exported cycle artifact already contains scores and distribution rows, treat it as the proposed source of truth, then audit it against evidence. Do not invent new scoring unless the source is missing or the request asks for recomputation.
