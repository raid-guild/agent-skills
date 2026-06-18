---
name: bankr-ops
description: Use this skill when Codex needs to reason about or prepare safe Bankr CLI operations such as checking Bankr status, drafting Bankr prompts, explaining token launch/fee/LLM wallet flows, or preparing reviewed commands. This skill must not execute financial, token launch, trading, fee-claim, or wallet actions without explicit human approval.
---

# Bankr Ops

Use this skill for conservative Bankr-related operations inside Prism.

Bankr source:

- Skill page: https://skills.bankr.bot/skills/bankr
- Provider: BankrBot
- Provider site: https://bankr.bot/
- Docs: https://docs.bankr.bot

Bankr describes the skill as a way to launch a token, earn from trades, fund an agent, and use a Bankr wallet with guardrails such as IP whitelisting, hallucination guards, and transaction verification.

## Core Commands From Bankr Catalog

Setup commands shown by the Bankr skill catalog:

```bash
npm install -g @bankr/cli
bankr login email you@example.com
bankr whoami
bankr prompt "Buy $50 of ETH on Base"
```

Example Bankr operations shown by the catalog:

```bash
# Launch a token on Base for free
bankr launch

# Track and claim trading fee revenue
bankr fees
bankr fees claim 0xYourToken

# Fund an agent's intelligence
bankr llm setup
bankr prompt "What tokens are trending on Base?"
```

## Safety Rating Note

The Bankr catalog lists an overall rating of `clean`, with a low-severity security finding:

- API key exposure risk in verbose logs.
- Debug logging may include API key values in plaintext when verbose mode is enabled.
- Avoid verbose logs when secrets are present.
- Never paste raw keys into chat or artifacts.

## Allowed Without Extra Approval

Codex may do these without additional approval when the user asks:

- Explain what Bankr is and what commands would be used.
- Inspect whether the `bankr` CLI appears installed.
- Prepare command plans without running them.
- Run non-mutating status/help commands such as:
  - `bankr --help`
  - `bankr whoami`
  - `bankr fees` only if it is confirmed to be read-only in the installed CLI version.
- Draft Bankr prompts for human review.
- Create Prism requests or artifacts describing proposed Bankr actions.

## Requires Explicit Human Approval Every Time

Do not execute these unless the user explicitly approves the exact action in the current conversation or workflow gate:

- `bankr login`
- `bankr launch`
- Any token creation, launch, or migration.
- Any trade, swap, buy, sell, transfer, approval, claim, bridge, mint, burn, or staking action.
- `bankr fees claim ...`
- `bankr llm setup` if it funds or configures a wallet/spending source.
- Any command that can move funds, create assets, change wallet state, or publish a token.
- Any command that exposes, stores, or requests credentials/secrets.

For these actions, restate:

- exact command
- network/chain
- wallet or account context, if known
- asset/token address, if any
- expected effect
- risk and reversibility
- whether public posting or onchain action will happen

Then wait for approval.

## Forbidden Behavior

Never:

- Invent that a Bankr action succeeded without command/API evidence.
- Store private keys, seed phrases, API keys, or auth links in Prism Memory, knowledge docs, GitHub, Discord, artifacts, or logs.
- Run commands with verbose/debug logging when secrets may appear.
- Treat model output from `bankr prompt` as financial advice.
- Execute financial/onchain actions from an unreviewed scheduled task.
- Let a Discord message alone authorize an irreversible onchain action unless the workflow has an explicit human gate and the user has approval authority.

## Operational Pattern

For requested Bankr actions:

1. Classify the request as read-only, planning, or mutating.
2. For read-only/planning, proceed conservatively and summarize findings.
3. For mutating/financial/onchain actions, prepare a reviewed action plan and stop for approval.
4. If approved, run the smallest exact command needed.
5. Capture transaction IDs, token addresses, URLs, or command output as request artifacts or external refs when operating through a Prism workflow.
6. Report failures directly and do not retry mutating actions unless the user explicitly approves retry.

## Integration With Prism

For workflow-backed requests:

- Use `change-request-ops` for tracked work.
- Store durable command plans or results as artifacts.
- Attach external refs for live onchain transactions, token pages, Bankr URLs, or GitHub records when available.
- Use `public-social-output-sanitizer` before publishing any public announcement about a Bankr action.

## Recommended First Use

Before any real Bankr operation, run only discovery commands:

```bash
bankr --help
bankr whoami
```

If the CLI is missing, propose installation but do not install unless the user asks.
