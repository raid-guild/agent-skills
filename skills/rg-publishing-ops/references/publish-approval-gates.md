# Publish Approval Gates

Use this before any live publishing action.

## Gate Checklist

Before `QUEUE`, `SEND`, `PUBLISH`, or marking an item `published`, confirm:

- exact content
- exact destination/account/channel
- exact operation
- timing or schedule
- public safety result
- approval status
- source/evidence status
- rollback or correction path, if any

## Requires Explicit Approval

Require explicit approval in the current request or workflow gate for:

- public X posts, replies, quotes, and scheduled queue entries
- Discord sends to public/community channels
- official announcements
- client-related claims
- governance, treasury, membership, or token content
- production/security claims
- publishing as Queen Raida or official RaidGuild accounts
- marking content as published without a live URL

## Safe Without Extra Approval

Usually safe when requested:

- inspect publishing queues
- inspect Bard Calendar records
- prepare publishing plans
- draft payloads
- reconcile already-known live URLs
- report status

## Stop Conditions

Stop and ask for approval or source clarification when:

- destination is vague
- account/persona is ambiguous
- content has not passed public safety
- live action is irreversible or externally visible
- source support is missing
- workflow state does not show an approved publish step
