# Collect Cycle Activity

Gather the raw evidence for the requested participation cycle.

## Use

- `prism-api-reader` for Prism Memory meeting artifacts, Prism Knowledge docs, raid/cohort artifacts, and historical references.
- `cookiejar-activity-reader` only when CookieJar evidence is explicitly requested or useful as optional historical context.

## Cycle detection

Identify the requested cycle key and window from the request, source artifact, or HallMonitor export. Examples:

- `AprMay2026`: 2026-04-01 through 2026-05-31.

Do not default to UTC month boundaries unless the request explicitly asks for a monthly historical cycle.

## Primary HallMonitor source

Use the current Participation Steward source model:

- Source workbook: `source/ParticipationSteward.xlsx`
- Exported cycle artifact: `docs/participation-steward/<cycle>.md`

Prefer the exported markdown cycle artifact for auditability. Use workbook data if the export is missing, incomplete, or needs regeneration.

## Required artifacts

Write artifacts that capture the cycle window and raw evidence used:

- `activity-report.md`
- `activity-report.json`
- `cycle-source.md` or equivalent extracted source artifact
- `evidence-index.json` mapping each recipient and score lane to cited evidence

If CookieJar is used, write optional artifacts such as `cookiejar-withdrawals.json` and clearly mark them as historical/optional evidence.

## Rules

- Resolve wallet-to-Discord identity through the Participation Steward export and HallMonitor data when possible.
- Call out unresolved identities instead of guessing.
- Verify cited Prism artifact IDs exist when the cycle artifact references them.
- Distinguish direct Prism evidence from manual role/steward confirmations.
- If a source is sparse or unavailable, say so in the artifact rather than silently omitting it.
