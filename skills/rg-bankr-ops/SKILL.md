---
name: rg-bankr-ops
description: Use when Codex needs to explain, inspect, plan, verify, or execute operator-approved Bankr operations, including Bankr CLI status, Bankr prompts, token launch planning, fee checks or claims, wallet/LLM setup, trading prompt review, command preparation, and post-action evidence capture. Proceed on read-only and planning tasks when requested; verify exact parameters before login, token launch, wallet funding, trading, transfers, fee claims, or any command that can move funds, create assets, expose credentials, or change wallet/token state.
---

# RaidGuild Bankr Ops

Use this skill as an execution assistant for authorized Bankr operators.

Bankr and underlying wallet/chain systems may have safeguards. This skill adds operator-intent verification so commands match the intended account, chain, asset, effect, and timing.

## Operating Model

Proceed when requested for:

- explaining Bankr concepts
- checking whether the CLI exists
- running help/status commands
- drafting Bankr prompts
- preparing command plans
- inspecting read-only fee/status information when confirmed read-only

Verify exact parameters immediately before:

- login or auth flows
- token creation or launch
- trades, swaps, buys, sells, transfers, approvals, bridges, mints, burns, staking
- fee claims
- wallet funding or LLM wallet/spending setup
- commands that expose, store, or request credentials/secrets

If the operator already gave exact command, target, and approval in the current context, proceed. Surface only mismatches, missing parameters, credentials risk, or irreversible/external effects.

## Routing

Read only the references needed:

- Operator verification: `references/operator-verification.md`
- Bankr commands: `references/bankr-commands.md`
- Evidence and public-output handling: `references/evidence-and-announcements.md`

Use `rg-public-output-safety` before publishing public announcements about Bankr actions.
Use `rg-publishing-ops` for sending or scheduling those announcements.

## Defaults

- Do not run verbose/debug logging when secrets may appear.
- Do not paste or store raw keys, seed phrases, auth links, cookies, or API tokens.
- Do not treat model output from `bankr prompt` as financial advice.
- Do not execute Bankr actions from an unreviewed scheduled task.
- Do not retry mutating actions unless the operator explicitly asks after seeing the failure.

## Output

For command plans:

```text
Bankr operation plan:
- command:
- account/wallet context:
- chain/network:
- asset/token:
- expected effect:
- verification needed:
- credential/logging risk:
- evidence to capture:
```

For completed operations, capture relevant ids, tx hashes, token addresses, Bankr URLs, and safe summaries.
