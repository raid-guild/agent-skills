# CRM Document Ingest

Use for NextCRM document upload handoff events.

## Required Artifacts

Create exactly:

1. `crm-document-received.json`
2. `crm-document-enrichment.md`

Do not use alternate artifact names.

## Payload Shape

The hook payload may be top-level or under `payload`.

Expected payload:

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
- This workflow does not write back to CRM unless explicitly updated.
- Do not duplicate full document text in markdown artifacts unless necessary.

## `crm-document-received.json`

Include normalized document metadata:

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

Use `null` for absent optional fields.

## `crm-document-enrichment.md`

Include:

- document id
- document name
- MIME type
- source URL if present
- content hash if present
- CRM-provided summary if present
- CRM-provided system type if present
- 3-5 bullet operational summary based on `contentText`
- suggested tags
- obvious follow-up actions

If `contentText` is missing or empty, record that clearly and complete gracefully.
