---
name: dao-proposal-watcher
description: Use this skill when Codex is asked to create, run, or maintain an instance-local watcher for DAOhaus or Moloch v3 proposals, especially scheduled tasks that detect new proposals and return a notification brief for Prism task delivery.
---

Use this skill to run or maintain a durable proposal watcher in this Prism instance.

The watcher polls a DAOhaus/Moloch v3 proposal subgraph, compares results against a local checkpoint, writes proposal reports to markdown, and returns a concise notification for any new proposals. Prism task-runner can deliver that returned text to Discord or another adapter through `outputConfig.outputDestinations`.

Do not store executable code in a Prism task row. Keep code in the instance volume and create scheduled tasks that invoke it.

## Files

Default persistent paths:

- Script: `<instance-custom-data>/dao-proposals/scripts/dao_proposal_watcher.mjs`
- Checkpoint: `<instance-custom-data>/dao-proposals/checkpoint.json`
- Reports: `<instance-custom-data>/dao-proposals/proposals/*.md`

If running locally outside Railway, the script also works with relative paths by setting `DAO_PROPOSAL_STATE_DIR`.

## Environment

Required:

- `DAOHAUS_GRAPHQL_ENDPOINT`: DAOhaus/Moloch v3 subgraph GraphQL endpoint.
- `DAOHAUS_DAO_ID`: DAO address/id, lowercased before querying.

Optional:

- `DAOHAUS_CHAIN_ID`: default `100`.
- `DAOHAUS_PROPOSAL_LIMIT`: default `15`.
- `DAOHAUS_PUBLIC_BASE_URL`: default `https://admin.daohaus.club`.
- `DAO_PROPOSAL_STATE_DIR`: default `<instance-custom-data>/dao-proposals`.

## Run

Use:

```bash
node <instance-custom-data>/dao-proposals/scripts/dao_proposal_watcher.mjs
```

If required config is missing, fail clearly and list the missing variable. Do not ask follow-up questions during scheduled runs.

## Scheduled Task Prompt

Use this prompt for a `codex-prompt` task:

```text
Use the dao-proposal-watcher skill. Run `node <instance-custom-data>/dao-proposals/scripts/dao_proposal_watcher.mjs`. Return the script output as the task result. If it reports new DAO proposals, include the proposal titles, statuses, links, and short descriptions. Do not ask follow-up questions.
```

If the user wants Discord delivery, resolve the channel at task creation time and store it in `outputConfig.outputDestinations`. Do not hard-code Discord posting inside the script unless the user explicitly asks to bypass Prism task output delivery.
