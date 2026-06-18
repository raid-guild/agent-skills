# Operator Verification

Use this before live Bankr operations.

The agent is a tool for the operator. Verification catches command/parameter mismatches; it does not re-litigate operator judgment.

## Proceed Without Extra Verification

Proceed when requested for:

- explanations
- CLI presence checks
- help/status commands
- command planning
- Bankr prompt drafting
- read-only fee/status inspection when confirmed read-only

## Verify Exact Parameters

Before live wallet/token/financial actions, restate:

- exact command or prompt
- account/wallet context, if known
- chain/network
- asset or token address
- amount
- expected effect
- whether funds, wallet state, token state, or public market artifacts may change
- credential/logging risk
- evidence to capture

If the operator has already provided exact command and approval in the current context, proceed. If parameters are vague, ask for the missing piece.

## Stop Conditions

Stop for clarification when:

- command can move funds but amount/asset/chain is unclear
- token address is shortened or ambiguous
- auth flow may expose credentials
- verbose/debug logs may include secrets
- command does more than the operator requested
- failure retry would repeat a mutating action
