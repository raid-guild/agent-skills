---
name: x-draft-queue
description: Use this skill when Codex needs to add, inspect, reset, or explain the autonomous X draft queue that posts one queued draft every six hours.
---

# X Draft Queue

Use this skill to manage the autonomous X posting queue for public posts, replies, and quote posts.

Queue storage: `<instance-custom-data>/x-draft-queue/drafts.json`
Scheduled task script key: `x-draft-queue-poster`
Scheduled task key: `x-draft-queue-poster-every-6h`

The task posts at most one eligible queued draft per run, every six hours. There is no human review gate by design, so only queue text that is already approved for public posting.

Draft records use this schema:

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

Supported kinds: `post`, `reply`, `quote`.

When adding drafts, treat text as public output, reject secrets/private notes/unsupported claims, compute a duplicate hash from kind + text + reply target + quote target, and do not add duplicate non-failed drafts.

When asked for status, report queued/sent/failed/skipped counts, the next eligible queued draft, and the last five sent tweet ids/URLs.

Do not automatically retry failed drafts. Only reset a failed or skipped draft to queued when the user explicitly asks.
