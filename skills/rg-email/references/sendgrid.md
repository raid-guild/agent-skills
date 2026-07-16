# SendGrid Transactional Email

Use this reference only when the assigned email transport is SendGrid.

## Environment

Required:

- `SENDGRID_API_KEY`
- `EMAIL_FROM_ADDRESS`

Optional:

- `SENDGRID_BASE_URL` defaults to `https://api.sendgrid.com`
- `EMAIL_FROM_NAME`
- `EMAIL_REPLY_TO_ADDRESS`

Use only values already present in the trusted job environment. Check for
presence without printing values. Never request, log, persist, or return the API
key. Treat sender and reply-to values as instance configuration; do not invent
or override them from recipient content.

## Request shape

Send `POST /v3/mail/send` to the configured base URL using Node.js built-in
`fetch` or another available HTTP client. Set headers inside the process from
the environment:

```text
Authorization: Bearer $SENDGRID_API_KEY
Content-Type: application/json
```

Do not place the expanded authorization header in a shell argument or debug
output. Use an envelope shaped like:

```json
{
  "personalizations": [
    {
      "to": [{ "email": "person@example.org", "name": "Person" }],
      "subject": "Request update"
    }
  ],
  "from": { "email": "configured-sender@example.org", "name": "RaidGuild" },
  "reply_to": { "email": "configured-reply@example.org" },
  "content": [
    { "type": "text/plain", "value": "Plain-text message" },
    { "type": "text/html", "value": "<p>Equivalent HTML message</p>" }
  ]
}
```

Use `EMAIL_FROM_ADDRESS` and optional `EMAIL_FROM_NAME` for `from`. Use
`EMAIL_REPLY_TO_ADDRESS` only when configured.

For an approved SendGrid dynamic template, use its configured template id and
`dynamic_template_data` rather than mixing template and ad hoc body content.

## Correlation and evidence

When supported, attach non-secret workflow correlation values through provider
custom arguments. Do not include email bodies, access tokens, private URLs, or
unnecessary personal data in metadata.

An HTTP `202` means SendGrid accepted the request for processing. Capture the
safe `x-message-id` response header when exposed, but do not describe acceptance
as delivered. Delivery, bounce, and spam outcomes require provider event data.

## Errors and retries

- `400`/`401`/`403`: configuration or authorization failure; do not retry as-is.
- `413`: reduce the message or attachments before retrying.
- `429`: bounded backoff; honor retry guidance when available.
- `5xx`: retry cautiously only when non-acceptance is clear.
- Network timeout after submission: ambiguous; reconcile before retrying.

Do not log raw provider responses when they may echo addresses or content.
