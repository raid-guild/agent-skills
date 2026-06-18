# Live URL Reconciliation

Use after a publish or send operation to update planning records and report evidence.

## Evidence To Capture

- live URL
- platform id
- account/persona
- destination/channel
- publish timestamp
- source draft or calendar event id
- response status
- failure body when safe

## Calendar Updates

When reconciling Bard Calendar:

- patch `live_url` when known
- set `status: published` only with live URL, external evidence, or explicit user confirmation
- preserve draft URL, owner, campaign, and human-authored notes
- add failure notes without exposing tokens or private request payloads

## Queue Updates

For queues:

- update sent/failed status
- attach tweet id/URL when available
- do not retry failed entries automatically
- preserve error summary without secrets

## Failure Handling

Report:

- operation attempted
- safe failure summary
- whether retry is safe
- whether content, auth, destination, rate limit, or API shape caused the issue
- what approval is needed before retry
