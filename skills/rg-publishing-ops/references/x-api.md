# X API Operations

Use this as a routing reference for X operations. Prefer current official X Developer API docs for implementation details when building or debugging API calls.

## Common Operations

- search posts
- look up users
- publish posts
- delete posts
- reply or quote
- manage follows
- inspect rate limits
- handle OAuth

## Safety Rules

- Verify posting account before publishing.
- For Queen Raida, expected account is `@raidguildish` unless explicitly approved otherwise.
- Do not post/delete/follow/DM without explicit approval or an approved workflow step.
- Public text must pass `rg-public-output-safety`.
- Capture tweet id, URL, account, and request context after publish.
- Do not expose OAuth tokens, bearer tokens, cookies, or auth URLs.

## When To Keep Separate

If X API implementation detail grows large or needs official-doc tracking, split this into a dedicated external/tool skill and keep `rg-publishing-ops` as the approval/orchestration layer.
