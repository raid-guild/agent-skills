# Ingest CRM Document

Use `rg-crm-ops`.

Read the handoff payload, document id, file metadata, target CRM entity ids, upload source, and request context.

Produce normalized metadata and enrichment artifacts with:

- CRM document id
- linked account/contact/lead/opportunity/project ids
- file name, type, size, and storage reference
- extracted title/summary when available
- privacy classification
- missing entity links or enrichment failures

Do not expose private document contents in public artifacts. Do not infer entity relationships not present in the payload or CRM lookup.
