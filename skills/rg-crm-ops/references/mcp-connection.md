# MCP Connection

Nexus CRM / NextCRM supports Streamable HTTP and SSE transports.

Canonical source:

- repo: `https://github.com/raid-guild/nexus-crm`
- local checkout when available: `/home/dekanjbrown/Projects/raidguild/nextcrm`
- route implementation: `app/api/mcp/[transport]/route.ts`
- auth/tool implementation: `lib/mcp/`

Prefer the repo implementation for current behavior if this reference and the app diverge.

## Streamable HTTP

```json
{
  "mcpServers": {
    "nextcrm": {
      "type": "http",
      "url": "https://YOUR_NEXTCRM_URL/api/mcp/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_TOKEN"
      }
    }
  }
}
```

## SSE

```json
{
  "mcpServers": {
    "nextcrm": {
      "type": "sse",
      "url": "https://YOUR_NEXTCRM_URL/api/mcp/sse",
      "headers": {
        "Authorization": "Bearer YOUR_API_TOKEN"
      }
    }
  }
}
```

## Auth

Tokens are generated from Profile > Developer > API Tokens.

- token prefix: `nxtc__`
- raw value shown only once at creation
- do not expose token in output, logs, docs, or artifacts
