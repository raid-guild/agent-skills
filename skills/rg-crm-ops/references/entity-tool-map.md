# Entity Tool Map

Use this as a quick Nexus CRM / NextCRM MCP routing map.

Canonical source:

- `https://github.com/raid-guild/nexus-crm`
- local implementation: `/home/dekanjbrown/Projects/raidguild/nextcrm/lib/mcp/tools/`

If tool names or schemas differ, use the repo implementation as source of truth.

## CRM Entities

Common tool families:

- accounts: list, get, search, create, update, delete
- contacts: list, get, search, create, update, delete
- leads: list, get, search, create, update, delete
- opportunities: list, get, search, create, update, delete
- targets: list, get, search, create, update, delete
- products: list, get, create, update, delete
- contracts: list, get, create, update, delete
- activities: list, get, create, update, delete
- documents: list, get, create, upload/download URL, link, unlink, delete
- target lists: list, get, create, update, delete, add/remove members
- enrichment: enrich contact/target, single or bulk
- email accounts: list
- campaigns: list, get, create, update, delete, send, pause, resume, templates, steps, stats
- projects: boards, sections, tasks, comments, document assignment
- reports: list, run

## Destructive Or External Actions

Verify before:

- soft delete
- campaign send
- pause/resume live campaign
- bulk enrichment
- document unlink/delete
- project/task deletion
- exporting private CRM data

## Common Workflows

- research company and create account/contact/activity
- build prospecting campaign
- track opportunity pipeline
- enrich targets or contacts
- manage project boards and tasks
- run reports
