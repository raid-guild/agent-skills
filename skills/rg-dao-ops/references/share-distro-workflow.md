# Share Distro Workflow

Use for Participation Steward cycle share distro proposal preparation.

## Scope

The current workflow is participation-cycle based, not necessarily a UTC month.

Example:

- `AprMay2026`: 2026-04-01 through 2026-05-31

Do not infer UTC month boundaries unless the request is explicitly a historical monthly rerun.

## Primary Sources

- `source/ParticipationSteward.xlsx`
- exported cycle artifact such as `docs/participation-steward/<cycle>.md`

Use exported markdown as primary auditable input when available.

## Current Scoring Model

- Engagement: 20
- Stewardship: 60
- Contribution: 70
- Maximum cycle gain: 150

Do not use old Raid/RIP/CookieJar/Meeting weights unless explicitly requested for historical rerun.

## Required Artifacts

Evidence:

- `activity-report.md`
- `activity-report.json`
- `cycle-source.md`
- `evidence-index.json`

Distro:

- `share-distro.md`
- `share-distro.json`

Proposal:

- `proposal-draft.md`
- `proposal-payload.json`
- `unsigned-tx.json` when build-only is available

Review:

- `discord-draft.md`

Submission:

- tx hash
- proposal id
- DAOhaus proposal URL
- final submitted payload

## Review Gate

Approval should verify:

- cycle key and date window
- primary source artifact/workbook
- scores match reviewed cycle artifact
- evidence supports scoring
- CookieJar evidence is optional/historical unless otherwise specified
- unresolved identity/scoring caveats are acceptable
- proposal payload matches the distro exactly

Before onchain submission, verify the approved distro and proposal payload still match exactly.
