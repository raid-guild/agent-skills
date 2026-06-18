---
name: raidguildish-x-activity-reporter
description: Use this skill when Codex needs to create a daily, weekly, or ad hoc X activity report for the RaidGuild account, store the report in Prism Memory, and prepare a concise Discord-ready summary.
---

# RaidGuildish X Activity Reporter

Use this skill to produce repeatable X activity reports for the RaidGuild X account, `@RaidGuildish`.

## Scope

Default report target:

- Account URL: `https://x.com/RaidGuildish`
- Account handle: `@RaidGuildish`
- Reporting window: current UTC day unless the task prompt provides another date range
- Primary output: concise Discord-ready report
- Persistent output: Prism Memory inbox item with structured metrics and human-readable summary

## Required companion skills

When available, use:

- `x-developer-api` to read X account and post metrics
- `prism-api-reader` to retrieve prior RaidGuildish reports for comparison
- `prism-api-writer` to store the new report in Prism Memory

Do not publish posts, replies, follows, likes, or other X actions. This skill is read/report only.

## Retrieval workflow

1. Resolve the current UTC date and reporting window.
2. Fetch the `@RaidGuildish` account snapshot from X:
   - followers
   - following
   - total posts
   - likes count
   - media count
3. Fetch authored X activity in the reporting window:
   - original posts
   - replies
   - quote posts
   - reposts, if visible
   - posts with media
4. Fetch per-post public metrics where available:
   - likes
   - replies
   - reposts
   - quotes
   - impressions, if available
5. Retrieve prior RaidGuildish X activity reports from Prism Memory when available and compute deltas:
   - follower delta
   - following delta
   - total post delta
   - likes-count delta
   - media-count delta
   - change in posting volume
6. Identify the best-performing authored post in the window and any notable recent baseline post if the window has no activity.

## Prism Memory write

Store each report as a memory inbox item.

Use these defaults unless the task prompt says otherwise:

- `source`: `x-api`
- `bucket`: `raidguildish`
- `type`: `x_activity_report`
- `author`: `raidguildish-x-activity-reporter`
- `ts`: report generation timestamp in ISO format

The `content` should contain a compact human-readable report and a structured JSON block with at least:

```json
{
  "account": "RaidGuildish",
  "handle": "@RaidGuildish",
  "account_url": "https://x.com/RaidGuildish",
  "date_utc": "YYYY-MM-DD",
  "window": {
    "start": "ISO timestamp",
    "end": "ISO timestamp"
  },
  "snapshot": {
    "followers": 0,
    "following": 0,
    "total_posts": 0,
    "likes_count": 0,
    "media_count": 0
  },
  "deltas": {},
  "activity": {
    "posts": 0,
    "replies": 0,
    "quotes": 0,
    "reposts": 0,
    "media_posts": 0
  },
  "engagement": {
    "authored_posts_engagement": 0,
    "top_posts": []
  },
  "notes": [],
  "recommendations": []
}
```

## Discord output format

Return only a concise report suitable for a Discord thread. Format metrics one per line for readability. Use this shape:

```text
RaidGuildish X Activity Report - YYYY-MM-DD UTC

Account: @RaidGuildish
URL: https://x.com/RaidGuildish
Followers: <number> (<delta if available>)
Following: <number> (<delta if available>)
Total posts: <number> (<delta if available>)
Account likes count: <number> (<delta if available>)
Media count: <number> (<delta if available>)

Activity today:
Posts: <number>
Replies: <number>
Quotes: <number>
Reposts: <number>
Media posts: <number>

Engagement today:
Authored-post engagement: <number>
Top post: <url or no authored posts in this window>
Top post metrics: <likes>, <replies>, <reposts>, <quotes>, <impressions if available>

Notes: <short note or none>
Recommendation: <one short recommendation or none>
```

Keep every metric on its own line. Avoid dense comma-separated metric blocks except inside the single `Top post metrics` line. Do not include local file paths, API keys, debug logs, raw endpoint URLs, or internal execution notes.
