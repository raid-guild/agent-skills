# X Draft Queue

Use this for the autonomous X draft queue.

Queue storage:

```text
<instance-custom-data>/x-draft-queue/drafts.json
```

Scheduled task:

- script key: `x-draft-queue-poster`
- task key: `x-draft-queue-poster-every-6h`

The task posts at most one eligible queued draft every six hours.

## Hard Rule

There is no human review gate by design. Only add text that is already approved for public autonomous posting and has passed `rg-public-output-safety`.

## Draft Schema

```json
{
  "id": "xdq_...",
  "text": "post text",
  "kind": "post",
  "reply_to_tweet_id": null,
  "quote_tweet_id": null,
  "status": "queued",
  "created_at": "2026-05-29T00:00:00.000Z",
  "scheduled_after": null,
  "sent_at": null,
  "tweet_id": null,
  "error": null,
  "hash": "sha256..."
}
```

Supported kinds:

- `post`
- `reply`
- `quote`

## Rules

- Reject secrets, private notes, unsupported claims, and unapproved persona/account claims.
- Compute duplicate hash from kind + text + reply target + quote target.
- Do not add duplicate non-failed drafts.
- Do not automatically retry failed drafts.
- Reset failed/skipped drafts only when explicitly requested.

## Status Reports

Report:

- queued/sent/failed/skipped counts
- next eligible queued draft
- last five sent tweet ids/URLs
