---
name: x-developer-api
description: Use when building with the X Developer API: searching posts, looking up users, streaming posts, publishing/deleting posts, managing follows, DMs, lists, spaces, trends, OAuth flows, and rate limits.
metadata:
    source: https://docs.x.com/skill.md
    upstream-name: X
    tested-posting-flow: OAuth 1.0a via api.twitter.com on 2026-05-19
---

# X Developer API Skill

## Product summary

The X API provides programmatic access to X's public conversation and user data through REST endpoints. Agents use it to search posts, retrieve user profiles, manage follows/blocks/mutes, stream real-time posts, publish content, manage direct messages, lists, spaces, and trends. The API uses pay-per-usage pricing (no subscriptions) and supports multiple authentication methods: Bearer Token (app-only), OAuth 1.0a (user context), OAuth 2.0 (user context), and Basic Auth (enterprise). Key files: Bearer Token from Developer Console, API keys/secrets for OAuth. Primary CLI: cURL or official SDKs (Python XDK, TypeScript XDK). Main docs: https://docs.x.com/x-api/introduction

## When to use

Reach for this skill when:
- Building applications that search, retrieve, or analyze posts (recent 7-day search or full-archive historical search)
- Looking up user profiles, managing follows, blocks, mutes, or user relationships
- Streaming real-time posts matching filter rules (filtered stream with up to 1,000 rules)
- Creating, editing, or deleting posts programmatically
- Managing direct messages, lists, spaces, or bookmarks
- Integrating X authentication into applications (OAuth flows, token management)
- Handling rate limits and pagination in production systems
- Accessing engagement metrics, trends, or community notes
- Building webhooks for real-time post delivery

Do not use for: X Ads API (separate product for ad campaigns), X for Websites (embedded posts/buttons), or authentication-only flows without API calls.

## Environment Variables

Use the names shown below when credentials come from the X Developer Console. Never hardcode credentials in code, prompts, artifacts, or logs.

### App-only public reads

- `X_BEARER_TOKEN`: Bearer Token for OAuth 2.0 app-only requests. Use for public reads such as user lookup, recent search, full-archive search, trends, and filtered stream.

### OAuth 1.0a user context / posting

Use this set for posting and other user-context actions. These values must all come from the same X app, and the access token must be regenerated after app permissions are set to Read and write.

- `X_CONSUMER_KEY`: Consumer Key from the OAuth 1.0a Keys section. Prefer this for signing OAuth 1.0a requests.
- `X_CONSUMER_SECRET`: Consumer Secret from the same OAuth 1.0a Keys section. Prefer this for signing OAuth 1.0a requests.
- `X_API_KEY`: accepted alias for `X_CONSUMER_KEY` when the console labels the same value API Key.
- `X_API_SECRET`: accepted alias for `X_CONSUMER_SECRET` / API Secret.
- `X_ACCESS_TOKEN`: Access Token for the target X account, such as `@raidguildish`.
- `X_ACCESS_TOKEN_SECRET`: Access Token Secret for the same target X account.

Working priority order for OAuth 1.0a signing:

1. `X_CONSUMER_KEY` + `X_CONSUMER_SECRET` + `X_ACCESS_TOKEN` + `X_ACCESS_TOKEN_SECRET`
2. `X_API_KEY` + `X_API_SECRET` + `X_ACCESS_TOKEN` + `X_ACCESS_TOKEN_SECRET`

Before posting, verify the token with `GET https://api.twitter.com/1.1/account/verify_credentials.json?skip_status=true&include_email=false`. Refuse to post if `screen_name` is not the expected account.

For OAuth 1.0a posting, the tested working endpoint is `POST https://api.twitter.com/2/tweets` with a JSON body such as `{"text":"Build With Humans"}`. Build the OAuth signature against the exact URL host used in the request.

### OAuth 2.0 user context / PKCE

- `X_CLIENT_ID`: OAuth 2.0 client ID / client key.
- `X_CLIENT_SECRET`: OAuth 2.0 client secret, when the app type uses one.
- `X_REDIRECT_URI`: registered OAuth callback URL.

OAuth 2.0 user context requires explicit scopes such as `tweet.read`, `tweet.write`, `users.read`, `offline.access`, and other endpoint-specific scopes.

### Naming rule

Prefer X Developer Console names for new work: `X_CONSUMER_KEY`, `X_CONSUMER_SECRET`, `X_ACCESS_TOKEN`, and `X_ACCESS_TOKEN_SECRET` for OAuth 1.0a. Treat `X_API_KEY` and `X_API_SECRET` as compatibility aliases. Do not introduce `TWITTER_*` names unless maintaining an existing deployment.

## Tested Prism Runtime Flow

On 2026-05-19, the Prism runtime successfully posted to `@raidguildish` using OAuth 1.0a with:

- `X_CONSUMER_KEY`
- `X_CONSUMER_SECRET`
- `X_ACCESS_TOKEN`
- `X_ACCESS_TOKEN_SECRET`

The successful sequence was:

1. Verify credentials with `GET https://api.twitter.com/1.1/account/verify_credentials.json?skip_status=true&include_email=false`.
2. Confirm `screen_name` equals the intended account.
3. Create a post with `POST https://api.twitter.com/2/tweets`.

Do not skip the verify step for publishing workflows.

## Quick reference

### Authentication methods

| Method | Use case | Credentials | Scope |
|:-------|:---------|:------------|:------|
| Bearer Token (OAuth 2.0 app-only) | Public data, no user context | `Authorization: Bearer $TOKEN` | Read public posts, users, trends |
| OAuth 1.0a user context | User-specific actions | API Key, Secret, User Token, User Secret | Read/write user data, DMs, bookmarks |
| OAuth 2.0 user context (PKCE) | Web/mobile apps, user sign-in | Authorization code flow | Read/write user data with scopes |
| Basic Auth | Enterprise APIs only | Base64(email:password) | Enterprise endpoints |

### Common endpoints

| Task | Endpoint | Method | Auth |
|:-----|:---------|:--------|:-----|
| Look up user by username | `/2/users/by/username/{username}` | GET | Bearer Token |
| Get user by ID | `/2/users/{id}` | GET | Bearer Token |
| Search recent posts (7 days) | `/2/tweets/search/recent` | GET | Bearer Token |
| Search full archive | `/2/tweets/search/all` | GET | Bearer Token |
| Get post by ID | `/2/tweets/{id}` | GET | Bearer Token |
| Create post | `/2/tweets` | POST | OAuth 1.0a or 2.0 user |
| Delete post | `/2/tweets/{id}` | DELETE | OAuth 1.0a or 2.0 user |
| Get user's posts | `/2/users/{id}/tweets` | GET | Bearer Token |
| Get user's followers | `/2/users/{id}/followers` | GET | Bearer Token |
| Follow user | `/2/users/{id}/following` | POST | OAuth 1.0a or 2.0 user |
| Unfollow user | `/2/users/{id}/following/{target_user_id}` | DELETE | OAuth 1.0a or 2.0 user |
| Create filtered stream rule | `/2/tweets/search/stream/rules` | POST | Bearer Token |
| Connect to filtered stream | `/2/tweets/search/stream` | GET | Bearer Token |
| Get user's bookmarks | `/2/users/{id}/bookmarks` | GET | OAuth 2.0 user |
| Create bookmark | `/2/users/{id}/bookmarks` | POST | OAuth 2.0 user |

### Field parameters

Request additional data with field parameters. Each object type has its own parameter:

```bash
# Posts
?tweet.fields=created_at,public_metrics,author_id,lang

# Users
?user.fields=created_at,description,public_metrics,verified

# Media
?media.fields=url,preview_image_url,alt_text,public_metrics

# Polls
?poll.fields=voting_status,duration_minutes
```

### Rate limit headers

Every response includes:
- `x-rate-limit-limit` — Max requests in window
- `x-rate-limit-remaining` — Requests left
- `x-rate-limit-reset` — Unix timestamp when limit resets

Most endpoints reset every 15 minutes. Check headers proactively to avoid hitting limits.

### Pagination

Use `pagination_token` from response to fetch next page:

```bash
curl "https://api.x.com/2/tweets/search/recent?query=api&pagination_token=NEXT_TOKEN" \
  -H "Authorization: Bearer $TOKEN"
```

## Decision guidance

### When to use Bearer Token vs OAuth user context

| Scenario | Use Bearer Token | Use OAuth user context |
|:---------|:-----------------|:----------------------|
| Read public posts, users, trends | ✓ | ✓ |
| Create/delete your own posts | ✗ | ✓ |
| Access user's bookmarks, DMs | ✗ | ✓ |
| Follow/unfollow on behalf of user | ✗ | ✓ |
| Build public-only app | ✓ | ✗ |
| Build app requiring user sign-in | ✗ | ✓ |

### When to use recent search vs full-archive search

| Requirement | Recent search | Full-archive search |
|:------------|:--------------|:-------------------|
| Search last 7 days | ✓ | ✓ |
| Search older posts | ✗ | ✓ |
| Available to all developers | ✓ | Pay-per-use/Enterprise only |
| Max results per request | 100 | 500 |
| Query length | 512 chars | 1,024 chars |

### When to use filtered stream vs search

| Use case | Filtered stream | Search |
|:---------|:----------------|:-------|
| Real-time posts as published | ✓ | ✗ |
| Historical data lookup | ✗ | ✓ |
| Persistent connection | ✓ | ✗ |
| One-off queries | ✗ | ✓ |
| Up to 1,000 rules | ✓ | N/A |
| Webhook delivery option | ✓ | ✗ |

## Workflow

### Making your first API request

1. **Get credentials**: In Developer Console (console.x.com), create an app and copy the Bearer Token
2. **Choose endpoint**: Start with user lookup, post lookup, or recent search
3. **Build request**: Use cURL or SDK with Bearer Token in Authorization header
4. **Parse response**: Primary data is in `data` field; related objects in `includes`
5. **Add fields**: Use `tweet.fields`, `user.fields` parameters to request additional data
6. **Handle pagination**: Store `pagination_token` from response for next page
7. **Monitor rate limits**: Check `x-rate-limit-remaining` header; implement exponential backoff on 429 errors

### Searching posts

1. **Build query**: Use operators like `from:user`, `#hashtag`, `has:images`, `lang:en`, `-is:retweet`
2. **Choose endpoint**: Recent search (7 days) or full-archive search (historical)
3. **Set max_results**: Up to 100 for recent, 500 for full-archive
4. **Request fields**: Add `tweet.fields=created_at,public_metrics` for engagement data
5. **Paginate**: Use `pagination_token` to fetch next page
6. **Expand related data**: Use `expansions=author_id` and `user.fields` to get author details

### Streaming real-time posts

1. **Create rules**: POST to `/2/tweets/search/stream/rules` with rule value (e.g., `from:xdevelopers`)
2. **Verify rules**: GET `/2/tweets/search/stream/rules` to list active rules
3. **Connect to stream**: GET `/2/tweets/search/stream` with persistent connection
4. **Process posts**: Parse JSON objects from stream; blank lines are keep-alive signals
5. **Handle disconnections**: Reconnect if no data/keep-alive for 20+ seconds
6. **Manage rules**: Add/remove rules without disconnecting using POST/DELETE

### Publishing posts

1. **Authenticate**: Use OAuth 1.0a or OAuth 2.0 user context (not Bearer Token)
2. **Build payload**: Include `text` (required), optional `reply_settings`, `quote_tweet_id`, `reply` object
3. **POST to `/2/tweets`**: Send JSON body with post data
4. **Handle response**: Response includes new post ID and text
5. **Edit posts**: Use POST `/2/tweets/{id}` with `text` to edit (creates new ID, keeps edit history)
6. **Delete posts**: Use DELETE `/2/tweets/{id}`

### Managing user relationships

1. **Get followers/following**: GET `/2/users/{id}/followers` or `/2/users/{id}/following`
2. **Follow user**: POST `/2/users/{id}/following` with `target_user_id` in body
3. **Unfollow**: DELETE `/2/users/{id}/following/{target_user_id}`
4. **Mute user**: POST `/2/users/{id}/muting` with `target_user_id`
5. **Block user**: POST `/2/users/{id}/blocking` with `target_user_id`
6. **Check blocks/mutes**: GET `/2/users/{id}/blocking` or `/2/users/{id}/muting`

## Common gotchas

- **Bearer Token vs OAuth confusion**: Bearer Token is app-only (public data only). Use OAuth 1.0a or 2.0 for user-specific actions like creating posts or accessing bookmarks. Mixing them causes 403 Forbidden errors.
- **Missing fields in response**: By default, endpoints return minimal fields. Always add `tweet.fields`, `user.fields` parameters to get data you need. Missing fields appear as `null` or are omitted entirely.
- **Expansions without fields**: Using `expansions=author_id` includes the author object but returns only `id` and `username`. Add `user.fields=description,public_metrics` to get more author data.
- **Rate limit headers ignored**: Developers often ignore `x-rate-limit-remaining` and hit 429 errors. Check headers proactively and implement exponential backoff (wait 2s, then 4s, then 8s, etc.).
- **Pagination token expiration**: Pagination tokens expire after 30 minutes. If you pause between requests, regenerate the query instead of reusing old tokens.
- **Stream keep-alive signals**: Blank lines (`\r\n`) are sent every 20 seconds to keep connection alive. If you don't receive data or keep-alive for 20+ seconds, the connection is dead—reconnect.
- **Query length limits**: Recent search allows 512 characters; full-archive allows 1,024. Enterprise allows 4,096. Queries longer than the limit silently fail or return partial results.
- **Operator precedence**: Parentheses matter. `(A OR B) AND C` is different from `A OR (B AND C)`. Test complex queries in Postman first.
- **Retweets and replies included by default**: Use `-is:retweet` and `-is:reply` to exclude them. Many queries unintentionally include retweets.
- **User context required for DMs**: Direct messages require OAuth 1.0a or 2.0 user context. Bearer Token returns 403 Forbidden.
- **Post cap limits**: Pay-per-use accounts have monthly post caps. Filtered stream and search results count toward this cap. Check usage in Developer Console.
- **Edited posts create new IDs**: When a post is edited, a new ID is created. The `edit_history_tweet_ids` array shows all versions in order.

## Verification checklist

Before submitting work with the X API:

- [ ] **Authentication correct**: Bearer Token for public data, OAuth 1.0a/2.0 for user actions
- [ ] **Credentials not hardcoded**: Store tokens in environment variables, not in code
- [ ] **Fields requested**: Added `tweet.fields`, `user.fields` parameters for required data
- [ ] **Expansions paired with fields**: If using `expansions=author_id`, also added `user.fields`
- [ ] **Rate limits handled**: Implemented exponential backoff for 429 errors; checking `x-rate-limit-remaining` header
- [ ] **Pagination implemented**: Using `pagination_token` for multi-page results; not assuming all results fit in one request
- [ ] **Stream reconnection logic**: For filtered stream, reconnecting if no data/keep-alive for 20+ seconds
- [ ] **Error handling**: Catching 401 (auth), 403 (permissions), 404 (not found), 429 (rate limit), 500 (server errors)
- [ ] **Query tested**: Complex search queries tested in Postman or with sample data first
- [ ] **Operators valid**: Using only operators supported by endpoint (recent search vs full-archive have different limits)
- [ ] **User context scopes**: If using OAuth 2.0, verified app has required scopes (tweet.read, tweet.write, users.read, etc.)

## Resources

**Comprehensive navigation**: https://docs.x.com/llms.txt — Full page-by-page listing for all X API documentation

**Critical pages**:
1. [X API Introduction](https://docs.x.com/x-api/introduction) — Overview of all endpoints and features
2. [Make Your First Request](https://docs.x.com/make-your-first-request) — Step-by-step quickstart with cURL and code examples
3. [Authentication Overview](https://docs.x.com/fundamentals/authentication/overview) — All auth methods, when to use each, token management

---

> For additional documentation and navigation, see: https://docs.x.com/llms.txt
