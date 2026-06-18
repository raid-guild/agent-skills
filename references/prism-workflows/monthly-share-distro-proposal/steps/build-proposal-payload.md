# Build Proposal Payload

Prepare the DAO proposal package from the reviewed participation cycle distro inputs.

## Use

- `moloch-dao-ops` only as a narrow cycle distro proposal helper.
- Recent comparable share distro proposals from the DAO for structure and wording reference.

## Required artifacts

Write:

- `proposal-draft.md`
- `proposal-payload.json`
- `unsigned-tx.json` when a build-only unsigned transaction can be generated safely

## Required proposal shape

This step only needs to support the share distro proposal shape: minting shares to multiple recipient addresses according to the approved cycle distro artifact.

The payload artifacts should make it easy to inspect:

- DAO contract address
- chain id
- cycle key and date window
- recipient addresses
- share amounts per recipient
- total shares to mint
- proposal title and description
- calldata or action list used to construct the proposal transaction

## Rules

- Prefer the reviewed `share-distro.json` artifact as the source of truth for recipients and amounts.
- Reference known prior distro proposals when useful.
- Make sure the payload and distro artifact agree exactly on recipients and amounts.
- Do not broaden this step into arbitrary governance operations unless the workflow is revised.
