---
name: rg-dao-ops
description: Use when Codex needs to inspect, prepare, verify, or execute operator-approved RaidGuild DAO operations involving DAOhaus, Moloch v3, moloch-agent, governance proposal reads, proposal drafts, unsigned transaction artifacts, sponsoring, voting, processing, share distro proposals, proposal watchers, CookieJar participation evidence, or onchain governance reconciliation. Proceed on read-only, planning, and build-only tasks when requested; verify exact parameters before signing, broadcasting, voting, sponsoring, processing, or treasury/share-affecting actions.
---

# RaidGuild DAO Ops

Use this skill as an execution assistant for authorized DAO operators.

Protocol and smart contract safeguards are necessary, but this skill verifies operator intent, exact targets, payloads, source evidence, and external effects before live governance actions. Do not treat the operator as incapable; do prevent wrong-DAO, wrong-chain, wrong-recipient, wrong-proposal, or stale-state mistakes.

## Operating Model

Proceed when requested for:

- DAO inspection
- proposal/lifecycle reads
- treasury/member reads
- proposal drafting
- command planning
- build-only or unsigned transaction artifact generation
- evidence gathering
- watcher status/reporting

Verify exact parameters immediately before:

- signing or broadcasting transactions
- submitting proposals
- sponsoring, voting, cancelling, or processing proposals
- treasury, payment, shares, loot, token, or governance-setting changes
- any operation that becomes public, onchain, or governance-binding

If the operator already gave exact command, target, and approval in the current context, proceed. Surface only mismatches, missing parameters, stale state, or irreversible/external effects.

## Routing

Read only the references needed:

- Operator verification: `references/operator-verification.md`
- DAOhaus/Moloch CLI: `references/moloch-agent.md`
- Proposal watcher: `references/proposal-watcher.md`
- CookieJar evidence: `references/cookiejar-evidence.md`
- Share distro workflow: `references/share-distro-workflow.md`

Use `rg-publishing-ops` for Discord review posts or public announcements.
Use `rg-public-output-safety` before public publishing about DAO actions.

## Required Habits

- Use full `0x` addresses; never invent or expand shortened addresses.
- Re-read live proposal lifecycle before sponsor, vote, cancel, or process.
- Prefer build-only/unsigned artifacts for reviewable proposal prep.
- Save durable artifacts for distro, proposal, unsigned tx, tx hash, proposal id, and DAOhaus links.
- Treat CookieJar as read-only evidence unless a separate operator action explicitly concerns CookieJar administration.
- Keep public summaries no more specific than the onchain or source evidence.

## Output

For plans:

```text
DAO operation plan:
- operation:
- DAO:
- chain:
- command/payload:
- source evidence:
- current lifecycle/state:
- expected effect:
- verification needed:
- artifacts to save:
```

For completed live operations, record tx/proposal evidence and re-read final state when possible.
