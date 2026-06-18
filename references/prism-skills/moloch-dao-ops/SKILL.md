---
name: moloch-dao-ops
description: Use this skill when Codex needs to inspect a DAOhaus/Moloch DAO, prepare or submit governance proposals, sponsor/vote/process proposals, or generate unsigned transaction artifacts using the npm package @raidguild/meta-clawtel and its moloch-agent CLI.
---

# Moloch DAO Ops

Use this skill for DAOhaus / Moloch v3 governance operations in Prism workflows.

Primary runtime:

`npx -y @raidguild/meta-clawtel@0.3.12`

CLI command name:

`moloch-agent`

Install only if repeated use is expected:

`npm install -g @raidguild/meta-clawtel`

## Required environment

Reads only:
- `MOLOCH_SERVICE_URL` optional; default hosted service is acceptable
- `CHAIN_ID` optional; defaults to Base `8453`
- `RPC_URL` optional but recommended for reliable operation

Writes / onchain actions:
- `PRIVATE_KEY` required unless building unsigned tx artifacts only
- never send private keys to remote services

Useful defaults from CLI:
- hosted service handles Graph reads and IPFS pinning
- default service: `https://moloch-service-production.up.railway.app`
- default Base RPC: `https://mainnet.base.org`

## First checks

Run:

`moloch-agent health`
`moloch-agent capabilities`
`moloch-agent account`

Use these before any workflow step that may submit or sign transactions.

## Read commands

Use these for workflow evidence gathering and artifact prep:

`moloch-agent dao --dao 0xDAO`
`moloch-agent proposals --dao 0xDAO --first 100`
`moloch-agent proposal --dao 0xDAO --proposal 12`
`moloch-agent proposal-lifecycle --dao 0xDAO --proposal 12`
`moloch-agent process-queue --dao 0xDAO --first 100`
`moloch-agent members --dao 0xDAO --first 100`
`moloch-agent treasury-tokens --dao 0xDAO`
`moloch-agent balances --dao 0xDAO`
`moloch-agent daohaus-url --dao 0xDAO --proposal 12`
`moloch-agent links --dao 0xDAO --proposal 12`

## Proposal creation commands

Signal / text proposal:

`moloch-agent signal --dao 0xDAO --title "..." --description "..."`

Custom calldata proposal:

`moloch-agent custom-proposal --dao 0xDAO --title "..." --actions actions.json`

Treasury payment proposal:

`moloch-agent payment --dao 0xDAO --recipient 0xPAYEE --amount 0.01`

Direct shares / loot proposals:

`moloch-agent mint-shares --dao 0xDAO --to 0xMEMBER --amount 1`
`moloch-agent mint-loot --dao 0xDAO --to 0xMEMBER --amount 100`

Governance updates:

`moloch-agent gov-settings --dao 0xDAO --params gov-settings.json`
`moloch-agent token-settings --dao 0xDAO --pause-shares false --pause-loot false`

For proposal drafting without broadcast, add `--build-only` and save the returned unsigned transaction JSON as a workflow artifact.

## Lifecycle actions

Sponsor:

`moloch-agent sponsor --dao 0xDAO --proposal 12`

Vote with rationale:

`moloch-agent vote --dao 0xDAO --proposal 12 --approved true --reason "..."`

Cancel:

`moloch-agent cancel --dao 0xDAO --proposal 12`

Process exact proposal:

`moloch-agent process --dao 0xDAO --proposal 12 --proposal-data 0x...`

Process oldest ready proposal:

`moloch-agent process-ready --dao 0xDAO`

## Workflow expectations

For Prism workflows, prefer this split:
- read step: inspect DAO, proposals, treasury, members, links
- draft step: produce markdown/json artifacts and use `--build-only` when human review is required
- human gate: review the share distro report, proposal text, and unsigned tx artifacts
- submit step: broadcast only after approval
- reconcile step: re-read lifecycle state and attach DAOhaus/BaseScan links as external refs

## Artifacts to save

When used in a workflow, save durable artifacts for:
- activity report markdown
- share distro report markdown or csv
- proposal summary markdown
- onchain payload json
- unsigned transaction json when using `--build-only`
- post-submit receipt summary with proposal id, tx hash, and DAOhaus URL

## Safety rules

- Never broadcast a governance proposal before the workflow's human review gate passes.
- Never invent or expand shortened addresses; use full `0x` addresses only.
- Re-read live proposal lifecycle before sponsor, vote, cancel, or process actions.
- Prefer `--build-only` when the step is preparing reviewable artifacts.
- Use `vote --reason` when possible so the rationale is preserved.
- Treat ragequit and direct treasury actions as high-risk and irreversible.

## Monthly distro use

For monthly share distro workflows, this skill is best used for:
- reading DAO state and prior proposal context
- generating a draft payment / mint / custom proposal payload
- building unsigned transaction artifacts for review
- broadcasting the final approved proposal
- sponsoring, voting, or processing later if the workflow includes those steps
