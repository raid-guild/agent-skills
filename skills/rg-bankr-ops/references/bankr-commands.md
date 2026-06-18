# Bankr Commands

Bankr source references:

- `https://skills.bankr.bot/skills/bankr`
- `https://bankr.bot/`
- `https://docs.bankr.bot`

## Setup And Status

```bash
npm install -g @bankr/cli
bankr login email you@example.com
bankr whoami
bankr --help
```

`bankr login` is an auth flow; verify intent before running.

## Prompt

```bash
bankr prompt "Buy $50 of ETH on Base"
```

Treat prompt output as model/tool output, not financial advice.

## Token Launch

```bash
bankr launch
```

Verify exact launch intent, account, chain, token details, and public effect before running.

## Fees

```bash
bankr fees
bankr fees claim 0xYourToken
```

Only run `bankr fees` without extra verification if the installed CLI/version confirms it is read-only. Verify before `fees claim`.

## LLM Wallet Setup

```bash
bankr llm setup
```

Verify before running if it funds or configures a wallet/spending source.

## Logging

Avoid verbose/debug logs when secrets may appear. Do not paste raw keys, seed phrases, auth links, cookies, or API tokens into chat, artifacts, memory, GitHub, or Discord.
