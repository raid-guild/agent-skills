# Participation Cycle Share Distro Proposal

Use this workflow to prepare RaidGuild participation cycle share distro packages from the current Participation Steward evidence model, route the package through human review, and submit the approved proposal onchain.

This workflow keeps the historical key `monthly-share-distro-proposal` for compatibility, but the operating scope is now a participation cycle, not a UTC calendar month.

## Cycle Scope

The distro window is a configured cycle window. Examples:

- `AprMay2026` covers 2026-04-01 through 2026-05-31.
- Future cycles should use the source workbook/exported cycle artifact dates or the explicit request instructions.

Do not infer UTC month boundaries unless the requested cycle is actually a one-month cycle.

## Primary Sources

The current HallMonitor source of truth is the Participation Steward model:

- Source workbook: `source/ParticipationSteward.xlsx`
- Exported cycle artifact: `docs/participation-steward/<cycle>.md`, for example `docs/participation-steward/aprmay2026.md`

Use the exported cycle artifact as the primary auditable input when available. Use the workbook when the export is missing or needs regeneration. Historical monthly HallMonitor docs can be used only for context or prior patterns.

## Evidence Sources

Evidence may come from:

- Prism Memory meeting artifacts
- Prism Knowledge raid/cohort/project artifacts
- Hats, role, or steward confirmations
- DungeonMaster/cohort confirmations
- Human-provided notes in the cycle artifact
- CookieJar data as optional/historical evidence only

CookieJar is no longer a scoring lane by default.

## Participation Steward Scoring

Maximum gain per cycle: 150.

- Engagement: 20
- Stewardship: 60
- Contribution: 70

Do not use the old monthly HallMonitor model of Raid 40 / RIP 40 / CookieJar 10 / Meeting 10 unless the request explicitly asks for a historical monthly rerun.

## Output expectations

The workflow should produce durable artifacts rather than relying on chat text. At minimum, keep:

- an activity/evidence artifact
- a share distro artifact
- an onchain proposal payload artifact
- a Discord draft artifact for `#so-dev`

The Discord review report should explain Engagement, Stewardship, and Contribution for each recipient.

## Review and submission

No onchain submission should happen before the human review gate approves the artifacts.

The review gate should verify:

- the cycle key and date window are correct
- ParticipationSteward.xlsx or the exported cycle artifact is the primary source
- Engagement, Stewardship, and Contribution scores match the cycle artifact
- cited meeting, Hats, Prism, raid/cohort, DungeonMaster, or manual confirmations support the scores
- CookieJar is treated as optional/historical evidence, not a default scoring lane
- the proposal payload matches the reviewed distro exactly

After approval, submit onchain and record the resulting proposal URL, tx hash, and any DAOhaus link as durable evidence.
