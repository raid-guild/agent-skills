---
name: rg-crm-ops
description: Use when Codex needs to inspect, plan, or perform RaidGuild Nexus CRM / NextCRM operations through MCP or workflow artifacts, including accounts, contacts, leads, opportunities, targets, products, contracts, activities, documents, target lists, enrichment, email accounts, campaigns, projects, reports, CRM document upload handoffs, normalized document metadata, and CRM privacy-safe enrichment. Verify before destructive deletes, campaign sends, bulk enrichment, or privacy-sensitive writes.
---

# RaidGuild CRM Ops

Use this skill for RaidGuild Nexus CRM / NextCRM operations and CRM-related workflow handling.

This skill owns CRM MCP routing, entity operations, document handoffs, enrichment workflows, and privacy-safe CRM handling. It does not own public publishing, brand voice, or Portal CMS operations.

## Routing

Canonical app-specific source:

- Nexus CRM repo: `https://github.com/raid-guild/nexus-crm`
- Local checkout when available: `/home/dekanjbrown/Projects/raidguild/nextcrm`
- MCP implementation: `lib/mcp/` and `app/api/mcp/[transport]/route.ts`
- Agent guidance: `AGENTS.md`

For current MCP tool names, schemas, auth behavior, and endpoint implementation details, prefer the Nexus CRM repo over this distilled repo copy.

Read only the references needed:

- MCP connection and auth: `references/mcp-connection.md`
- Entity/tool map: `references/entity-tool-map.md`
- CRM document ingest: `references/document-ingest.md`
- Privacy and operator verification: `references/privacy-and-verification.md`

Use `rg-public-output-safety` before any CRM-derived content becomes public.
Use `rg-content-strategy` and `rg-brand-voice` for public-safe CRM-derived content.

## Operating Model

Proceed when requested for:

- read/list/search/get operations
- draft entity creation/update plans
- document handoff normalization
- enrichment summaries that do not expose private data publicly

Verify exact intent before:

- soft deletes
- campaign sends
- bulk enrichment
- CRM writes that affect client/prospect records
- document links/unlinks across sensitive entities
- exporting or sharing CRM-derived data

## Privacy Defaults

- Treat CRM data as private by default.
- Do not expose API tokens.
- Do not publish client/prospect/contact details unless approved.
- Do not duplicate full document text in artifacts unless necessary.
- Prefer summaries and metadata over raw content.

## Output

For plans:

```text
CRM operation plan:
- operation:
- entity:
- target record(s):
- data source:
- privacy considerations:
- verification needed:
- expected result:
```
