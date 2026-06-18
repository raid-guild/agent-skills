---
name: discord-send
description: Use this skill when Codex needs to send an approved message to Discord through the communication adapter, including normal channels and forum posts, after resolving an explicit output destination.
---

# Discord Send

Use this skill to send approved Discord output through the communication adapter from Codex Runtime.

This skill is for manual/operator sends and workflow steps where a Discord output destination is explicit. It does not replace task or workflow `outputConfig.outputDestinations`; prefer those for scheduled or workflow-owned delivery.

## Required Environment

- `COMMUNICATION_ADAPTER_BASE_URL`
- `COMMUNICATION_ADAPTER_TOKEN`

Send the adapter token as:

`X-Adapter-Token: <token>`

If a route also accepts bearer auth, `Authorization: Bearer <token>` is acceptable as an additional header.

## Safety Rules

1. Do not send public Discord messages unless the user explicitly asks to post/send, or the current workflow/task has an approved output destination and approval gate has passed.
2. For governance, treasury, membership, production, or public announcement content, restate the destination and content summary before sending unless the request is already in an approved publish step.
3. Never infer a destination from vague labels. Resolve the destination ID and type first.
4. For forum posts, require a title and body. Do not send a forum post as a normal channel message unless the user explicitly asks for that fallback.
5. Return the adapter response, message/thread URL when available, and any failure body exactly enough to debug.
6. Do not bypass source adapter access policy; this skill assumes the operator has already authorized the send context.

## Discover Destinations

Read available destinations:

`GET $COMMUNICATION_ADAPTER_BASE_URL/destinations`

Useful destination shape:

`{ adapter, platform, id, destinationId, type, name, label, parentId }`

Supported destination types expected here:

- `discord-channel`
- `discord-forum`

Known RaidGuild forum example:

`{ "adapter":"discord", "type":"discord-forum", "id":"1037470101718450288", "label":"Forum / 📜-rip-discussion" }`

When storing this in Prism task/workflow output config, use:

`{ "adapter":"discord", "type":"discord-forum", "id":"1037470101718450288", "label":"Forum / 📜-rip-discussion" }`

## Send Route

Adapter capabilities should advertise:

- `list-destinations`
- `send-message`
- route: `/messages`

Use:

`POST $COMMUNICATION_ADAPTER_BASE_URL/messages`

Headers:

`Content-Type: application/json`
`X-Adapter-Token: $COMMUNICATION_ADAPTER_TOKEN`

## Channel Message Payload

For a normal Discord channel, send a payload like:

```json
{
  "destination": {
    "adapter": "discord",
    "type": "discord-channel",
    "id": "123456789012345678"
  },
  "content": "Message body"
}
```

If the deployed adapter expects flattened fields instead, retry with:

```json
{
  "adapter": "discord",
  "type": "discord-channel",
  "destinationId": "123456789012345678",
  "content": "Message body"
}
```

## Forum Post Payload

For a Discord forum, prefer a title/body payload:

```json
{
  "destination": {
    "adapter": "discord",
    "type": "discord-forum",
    "id": "1037470101718450288"
  },
  "title": "Forum post title",
  "content": "Forum post body"
}
```

If the adapter expects flattened fields, retry with:

```json
{
  "adapter": "discord",
  "type": "discord-forum",
  "destinationId": "1037470101718450288",
  "title": "Forum post title",
  "content": "Forum post body"
}
```

## Suggested Workflow

1. Confirm the requested destination and send approval.
2. Call `GET /destinations` and match by exact destination ID or exact label.
3. Validate destination type.
4. Build channel or forum payload.
5. Call `POST /messages`.
6. Report the resulting URL/id or the failure response.

## Troubleshooting

- If the model can see destination metadata but cannot send, the transport adapter may not expose a callable send tool. From Codex Runtime, use the HTTP adapter route directly when env vars are present.
- If `discord-forum` is visible but send fails, confirm the adapter's `/messages` implementation supports forum thread creation, not only channel messages.
- If a workflow/task says no output destination is available, add the destination to that task/workflow's `outputConfig.outputDestinations`.
