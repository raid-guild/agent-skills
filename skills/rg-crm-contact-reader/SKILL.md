---
name: rg-crm-contact-reader
description: Use when Codex needs to list, retrieve, or search assigned RaidGuild Nexus CRM / NextCRM contacts through the Prism Gateway read capability.
metadata:
  gateway-capabilities:
    - crm.contact.read
---

# RaidGuild CRM Contact Reader

Use the assigned `crm.contact.read` capability for private, read-only NextCRM
contact queries. Do not read `NEXTCRM_API_TOKEN`, call the NextCRM MCP endpoint
directly, or fall back to runtime credentials.

Invoke the capability by posting to `$PRISM_RUNTIME_CAPABILITY_URL` with
`x-runtime-capability-token: $PRISM_RUNTIME_CAPABILITY_TOKEN`.

Supported input:

```json
{ "operation": "list", "limit": 20, "offset": 0 }
```

```json
{ "operation": "get", "id": "contact-uuid" }
```

```json
{ "operation": "search", "query": "name or email", "limit": 20, "offset": 0 }
```

Only `list`, `get`, and `search` are available. Use `rg-crm-ops` for other CRM
entities, planning, writes, enrichment, campaigns, documents, or reports.

Treat all returned contact data as private. Summarize only fields needed for the
request, do not publish contact details, and do not persist raw results into
public artifacts or memory.
