# Key And URL Policy

Use stable object keys when downstream systems need retry/reconciliation.

## Key Construction

Recommended key parts:

- configured prefix
- workflow key or project key
- request id or stable source id
- artifact id or content hash
- original filename or normalized filename

Example:

```text
<prefix>/<workflow-key>/<request-id>/<artifact-id>/<filename>
```

## Rules

- Avoid spaces and shell-sensitive characters.
- Preserve useful extensions.
- Use content hash when deduplication matters.
- Reuse the same key for reruns of the same approved artifact when appropriate.
- Do not include secrets, client-private names, or local filesystem paths in keys.

## Fetchable URLs

Return absolute `http(s)` URLs only when downstream services can fetch them without private headers.

If the bucket is private and only signed URLs are possible, record expiration and do not treat the URL as durable unless that is acceptable for the consumer.
