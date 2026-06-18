# Operator Verification

Use this before live DAO operations.

The agent is a tool for the operator. Verification exists to catch parameter mismatches, not to second-guess the operator's judgment.

## Proceed Without Extra Verification

Proceed when requested for:

- read-only DAO inspection
- proposal reads
- lifecycle/status reads
- treasury/member reads
- command planning
- proposal drafting
- build-only or unsigned transaction generation
- watcher reports
- CookieJar evidence reads

## Verify Exact Parameters

Before live onchain/governance action, restate:

- exact command or payload
- DAO address
- chain id/network
- proposal id, when applicable
- recipient addresses and amounts, when applicable
- expected effect
- lifecycle state just read
- whether a transaction will be signed or broadcast
- artifacts/evidence to save

If the operator has already provided exact parameters and current approval, proceed. If any parameter is vague or stale, ask for the missing piece.

## Mismatch Checks

Stop for clarification when:

- DAO address is shortened or ambiguous
- chain differs from expected context
- proposal lifecycle changed since the plan was prepared
- proposal id/title do not match
- recipient or amount differs from reviewed artifact
- command would sign/broadcast when the operator asked only for a draft
- private key or signer context is missing for a live action
