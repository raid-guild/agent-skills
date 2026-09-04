# Moloch Agent

Use for DAOhaus / Moloch v3 operations with `@raidguild/meta-clawtel`.

Primary runtime (pinned until the next npm release includes Gnosis support):

```bash
npm exec --yes \
  --package=https://github.com/HausDAO/moloch-agent/archive/ff0891b3dbfcbf2a4c6a58f75fac7b097134b91f.tar.gz \
  -- moloch-agent
```

Do not substitute `@raidguild/meta-clawtel@0.3.12` for Gnosis operations. That
release only signs direct transactions on Base. The pinned runtime supports
Base `8453` and Gnosis `100`.

CLI command:

```bash
moloch-agent
```

## Environment

Reads:

- `MOLOCH_SERVICE_URL` optional
- `CHAIN_ID` optional; defaults to Base `8453`; set it explicitly to `100` for Gnosis
- `RPC_URL` optional but recommended; use a reliable Gnosis RPC for chain `100`

Writes/onchain:

- `PRIVATE_KEY`, `WALLET_PRIVATE_KEY`, or `EVM_WALLET_PRIVATE_KEY` is required unless building unsigned tx artifacts only
- never send private keys to remote services

## First Checks

Run before any workflow step that may submit or sign:

```bash
moloch-agent health
moloch-agent capabilities
moloch-agent account
moloch-agent read-dao --dao 0xDAO
```

Before sending a Gnosis proposal, verify that the derived signer has enough
xDAI for gas and the Baal `proposalOffering`. Re-read the DAO immediately before
building and again immediately before broadcasting; do not assume the offering
or sponsorship threshold is unchanged.

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

For an approved proposal broadcast:

1. Rebuild or load the exact approved transaction artifact.
2. Confirm chain `100`, DAO address, destination, calldata, native value,
   recipients, token amounts, and expiration-sensitive quote inputs match the
   approval packet exactly.
3. If a quote, amount, calldata, or native value changed, return for fresh
   approval instead of signing the replacement.
4. Send with `--send`, wait for the receipt, and save the transaction hash.
5. Re-read `proposalCount` and the resulting proposal, then save the proposal
   id, DAOhaus URL, Gnosisscan URL, and receipt evidence.

## Lifecycle Commands

```bash
moloch-agent sponsor --dao 0xDAO --proposal 12
moloch-agent vote --dao 0xDAO --proposal 12 --approved true --reason "..."
moloch-agent cancel --dao 0xDAO --proposal 12
moloch-agent process --dao 0xDAO --proposal 12 --proposal-data 0x...
moloch-agent process-ready --dao 0xDAO
```

Re-read lifecycle before lifecycle actions.
