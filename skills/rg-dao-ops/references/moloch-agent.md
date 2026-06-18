# Moloch Agent

Use for DAOhaus / Moloch v3 operations with `@raidguild/meta-clawtel`.

Primary runtime:

```bash
npx -y @raidguild/meta-clawtel@0.3.12
```

CLI command:

```bash
moloch-agent
```

## Environment

Reads:

- `MOLOCH_SERVICE_URL` optional
- `CHAIN_ID` optional; defaults to Base `8453`
- `RPC_URL` optional but recommended

Writes/onchain:

- `PRIVATE_KEY` required unless building unsigned tx artifacts only
- never send private keys to remote services

## First Checks

Run before any workflow step that may submit or sign:

```bash
moloch-agent health
moloch-agent capabilities
moloch-agent account
```

## Read Commands

```bash
moloch-agent dao --dao 0xDAO
moloch-agent proposals --dao 0xDAO --first 100
moloch-agent proposal --dao 0xDAO --proposal 12
moloch-agent proposal-lifecycle --dao 0xDAO --proposal 12
moloch-agent process-queue --dao 0xDAO --first 100
moloch-agent members --dao 0xDAO --first 100
moloch-agent treasury-tokens --dao 0xDAO
moloch-agent balances --dao 0xDAO
moloch-agent daohaus-url --dao 0xDAO --proposal 12
moloch-agent links --dao 0xDAO --proposal 12
```

## Proposal Commands

Signal:

```bash
moloch-agent signal --dao 0xDAO --title "..." --description "..."
```

Custom calldata:

```bash
moloch-agent custom-proposal --dao 0xDAO --title "..." --actions actions.json
```

Payment:

```bash
moloch-agent payment --dao 0xDAO --recipient 0xPAYEE --amount 0.01
```

Shares/loot:

```bash
moloch-agent mint-shares --dao 0xDAO --to 0xMEMBER --amount 1
moloch-agent mint-loot --dao 0xDAO --to 0xMEMBER --amount 100
```

Use `--build-only` for reviewable artifacts without broadcast when supported.

## Lifecycle Commands

```bash
moloch-agent sponsor --dao 0xDAO --proposal 12
moloch-agent vote --dao 0xDAO --proposal 12 --approved true --reason "..."
moloch-agent cancel --dao 0xDAO --proposal 12
moloch-agent process --dao 0xDAO --proposal 12 --proposal-data 0x...
moloch-agent process-ready --dao 0xDAO
```

Re-read lifecycle before lifecycle actions.
