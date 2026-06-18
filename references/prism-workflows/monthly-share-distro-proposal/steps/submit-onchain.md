# Submit Onchain

Submit the approved participation cycle share distro proposal onchain.

## Use

- `moloch-dao-ops` as a narrow chain-aware submission helper.

## Before submitting

Verify again that:

- human review approved this exact cycle distro
- recipient addresses and amounts match `share-distro.json`
- total shares to mint matches the approved proposal payload
- proposal title/description reference the cycle key and date window

## Required outputs

Record durable evidence for:

- tx hash
- proposal id when available
- DAOhaus proposal URL when available
- final submitted payload

Do not submit any onchain transaction before approval. Do not submit if payload and reviewed distro differ.
