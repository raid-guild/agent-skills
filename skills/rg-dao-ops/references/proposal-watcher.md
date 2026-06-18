# Proposal Watcher

Use for durable DAOhaus/Moloch proposal watcher operations.

The watcher polls a DAOhaus/Moloch v3 proposal subgraph, compares against a local checkpoint, writes proposal reports to markdown, and returns notifications for new proposals.

## Files

Default persistent paths:

- Script: `<instance-custom-data>/dao-proposals/scripts/dao_proposal_watcher.mjs`
- Checkpoint: `<instance-custom-data>/dao-proposals/checkpoint.json`
- Reports: `<instance-custom-data>/dao-proposals/proposals/*.md`

For local runs, `DAO_PROPOSAL_STATE_DIR` may override state location.

## Environment

Required:

- `DAOHAUS_GRAPHQL_ENDPOINT`
- `DAOHAUS_DAO_ID`

Optional:

- `DAOHAUS_CHAIN_ID`, default `100`
- `DAOHAUS_PROPOSAL_LIMIT`, default `15`
- `DAOHAUS_PUBLIC_BASE_URL`, default `https://admin.daohaus.club`
- `DAO_PROPOSAL_STATE_DIR`

## Run

```bash
node <instance-custom-data>/dao-proposals/scripts/dao_proposal_watcher.mjs
```

If config is missing, fail clearly and list missing variables. Scheduled runs should not ask follow-up questions.

Use Prism task output destinations for Discord delivery instead of hard-coding Discord posting into the watcher unless explicitly requested.
