# SendGrid Through Gateway

Use this reference only when the assigned email transport is SendGrid.

## Credential boundary

The SendGrid API key belongs in Credential Gateway. Use the assigned email
toolset's canonical `describe` and `request` operations. Never read, print,
request, store, or transmit `SENDGRID_API_KEY` as task or model input.

The exact Gateway toolset key is instance configuration and must not be
hardcoded into this reusable skill.

## Request shape

After inspecting `describe`, use `request` to submit the provider request. A
typical SendGrid operation is `POST /v3/mail/send` with an envelope shaped like:

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

Follow the live toolset schema over this example. Use a verified sender identity
configured for the instance; do not invent a From address.

For an approved SendGrid dynamic template, use its configured template id and
`dynamic_template_data` rather than mixing template and ad hoc body content.

## Correlation and evidence

When supported, attach non-secret workflow correlation values through provider
custom arguments. Do not include email bodies, access tokens, private URLs, or
unnecessary personal data in metadata.

An HTTP `202` means SendGrid accepted the request for processing. Capture the
safe provider message id header when exposed, but do not describe acceptance as
delivered. Delivery, bounce, and spam outcomes require provider event data.

## Errors and retries

- `400`/`401`/`403`: configuration or authorization failure; do not retry as-is.
- `413`: reduce the message or attachments before retrying.
- `429`: bounded backoff; honor retry guidance when available.
- `5xx`: retry cautiously only when non-acceptance is clear.
- Network timeout after submission: ambiguous; reconcile before retrying.

Do not log raw provider responses when they may echo addresses or content.
