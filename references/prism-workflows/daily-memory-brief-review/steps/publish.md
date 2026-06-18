# Publish

Publish the approved daily brief into Payload CMS as a draft entry in the dailyBriefs collection.

## Required Environment

- PAYLOAD_CMS_BASE_URL
- PAYLOAD_CMS_EMAIL
- PAYLOAD_CMS_PASSWORD

Optional environment:

- PAYLOAD_CMS_USERS_LOGIN_PATH (default /api/users/login)
- PAYLOAD_CMS_DAILY_BRIEFS_PATH (default /api/dailyBriefs)

## Inputs

Use the latest approved brief draft and its source-summary context.

## Behavior

1. Log in to Payload CMS and get a JWT.
2. Build the dailyBriefs payload expected by the destination.
3. Create the entry as a draft or authenticated-only brief, following the destination schema.
4. Save a publish receipt as a request artifact containing at least the created Payload daily brief id, title, briefDate, and admin URL if available.

## Output

Return a concise publish summary with:

- daily brief id
- title
- briefDate
- visibility
- admin URL when available

If Payload credentials or payload construction are unavailable, return a clear blocked result rather than partially publishing.
