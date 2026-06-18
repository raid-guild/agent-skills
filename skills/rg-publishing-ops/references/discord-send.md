# Discord Send

Use this for approved Discord sends through the communication adapter.

## Environment

Require:

- `COMMUNICATION_ADAPTER_BASE_URL`
- `COMMUNICATION_ADAPTER_TOKEN`

Send:

```text
X-Adapter-Token: <token>
Content-Type: application/json
```

Do not expose the token.

## Rules

- Do not send unless the user explicitly asks, or the workflow has an approved destination and approval gate.
- Resolve exact destination id and type before sending.
- For governance, treasury, membership, production, security, client, or announcements, restate destination and content summary before sending unless already in an approved publish step.
- Forum posts require title and body.
- Return message/thread URL or id when available.

## Discover Destinations

```http
GET /destinations
```

Expected destination types:

- `discord-channel`
- `discord-forum`

## Send Route

```http
POST /messages
```

Channel payload:

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

Forum payload:

```json
{
  "destination": {
    "adapter": "discord",
    "type": "discord-forum",
    "id": "123456789012345678"
  },
  "title": "Forum post title",
  "content": "Forum post body"
}
```

If the adapter expects flattened fields, retry with `adapter`, `type`, `destinationId`, `title`, and `content`.
