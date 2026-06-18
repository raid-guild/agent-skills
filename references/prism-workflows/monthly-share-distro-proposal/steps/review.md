# Review

A human reviewer should verify the participation cycle distro artifacts and proposal payload before any onchain action.

## Approve only if

- the cycle key and configured date window are correct
- ParticipationSteward.xlsx or the exported `docs/participation-steward/<cycle>.md` artifact is the primary source
- Engagement, Stewardship, and Contribution scores match the reviewed cycle artifact
- cited Prism meeting artifacts, Hats/role records, raid/cohort artifacts, DungeonMaster/cohort confirmations, or manual confirmations support the scores
- CookieJar evidence, if present, is treated as optional/historical and not a default scoring lane
- unresolved identities or manual evidence caveats are acceptable for this cycle
- the proposal payload matches the reviewed distro exactly

## Routes

- `approved` continues to onchain submission
- `changesRequested` returns to cycle distro construction
- `rejected` closes the request
