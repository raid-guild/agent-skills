# Ingest CRM Document

## Required outcome

Read the request artifact named `hook-payload.json`. Create exactly these two durable artifacts, with these exact names:

1. `crm-document-received.json`
2. `crm-document-enrichment.md`

Do not use alternate names such as `crm-document-normalized.json`, `crm-document-intake-summary.md`, or any other filename.

After creating those exact artifacts, report completion.

## Payload shape

The NextCRM payload may appear either as the top-level JSON object or wrapped under a top-level `payload` key by the hook system. If `hook-payload.json` has `payload`, use `payload` as the NextCRM payload. Otherwise use the top-level object.

Expected NextCRM payload:

```json
{
  "source": "nextcrm",
  "event": "crm-document-uploaded",
  "document": {
    "id": "...",
    "name": "...",
    "mimeType": "...",
    "url": "...",
    "contentHash": "...",
    "summary": "...",
    "systemType": "..."
  },
  "contentText": "..."
}
```

## Constraints

- Do not require a target repository.
- Do not modify code.
- Do not call `/admin/*`.
- Use `/agent/*` APIs with `x-service-token` if API calls are needed.
- This version does not write back to CRM.
- Do not duplicate the full document text in markdown artifacts unless necessary.

## Required artifact: crm-document-received.json

Create `crm-document-received.json` as JSON. Include normalized document metadata:

```json
{
  "source": "nextcrm",
  "event": "crm-document-uploaded",
  "receivedAt": "<ISO timestamp>",
  "document": {
    "id": "...",
    "name": "...",
    "mimeType": "...",
    "url": "...",
    "contentHash": "...",
    "summary": "...",
    "systemType": "..."
  },
  "contentTextPresent": true,
  "contentTextLength": 1234
}
```

Use `null` for absent optional document fields.

## Required artifact: crm-document-enrichment.md

Create `crm-document-enrichment.md` as concise markdown. Include:

- document id
- document name
- MIME type
- source URL if present
- content hash if present
- CRM-provided summary if present
- CRM-provided system type if present
- a short 3-5 bullet operational summary based on `contentText`
- suggested tags
- obvious follow-up actions

If `contentText` is missing or empty, record that clearly and complete gracefully.
