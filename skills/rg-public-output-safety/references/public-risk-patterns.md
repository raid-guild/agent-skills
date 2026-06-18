# Public Risk Patterns

Use this to identify blockers before public output is posted, queued, sent, or marked ready for approval.

## Secrets And Credentials

Block or redact:

- API keys
- bearer tokens
- OAuth tokens
- private keys
- seed phrases
- passwords
- cookies
- service tokens
- webhook secrets
- signed URLs
- database URLs
- raw env var values

## Internal Infrastructure

Block or redact:

- localhost
- `127.0.0.1`
- private service URLs
- Railway/internal hostnames
- admin-only routes
- raw API routes
- service-token artifact URLs
- local filesystem paths
- stack traces
- command logs
- runtime paths

## Private Context

Block or require review for:

- private Discord details
- client names or work unless approved
- contributor private information
- meeting notes not approved for public use
- internal prompts or workflow instructions
- task ids and artifacts when not public
- financial, wallet, or governance details not already public-safe

## Unsupported Claims

Require source or soften/block claims about:

- dates
- pricing
- availability
- client approval
- partnerships
- funding
- governance outcomes
- member roles
- project status
- cohort admissions
- legal, financial, or security promises
- performance guarantees

## Persona And Account Mismatch

Watch for:

- Queen Raida / `@raidguildish` speaking as `@RaidGuild` HQ
- agent persona implying human membership
- agent persona claiming governance authority
- client commitments from the wrong account
- public copy that blurs draft vs approved statement

## Human Review Required

Escalate when output touches:

- governance
- treasury or financial actions
- client work
- security
- legal claims
- identity-sensitive information
- public publishing from an official or semi-official account
