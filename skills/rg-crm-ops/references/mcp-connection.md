# MCP Connection

Nexus CRM / NextCRM supports Streamable HTTP and SSE transports.

Trusted Prism jobs receive the instance connection through conventional
environment variables:

- `NEXTCRM_BASE_URL`
- `NEXTCRM_API_TOKEN`

Build the Streamable HTTP URL as `${NEXTCRM_BASE_URL}/api/mcp/mcp` after
removing a trailing slash. Send `Authorization: Bearer <token>` from inside the
client process. Never print, persist, or return the token. If either variable is
missing, report its name and direct the operator to instance credential
Settings; do not request the value in chat.

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
