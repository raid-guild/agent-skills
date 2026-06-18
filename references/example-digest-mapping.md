# Example Digest Mapping

This reference supports the exported `portal-ops-skill` instructions. It shows how source material can be mapped into Portal CMS primitives without inventing missing facts.

## Input Shape

```json
{
  "date": "2026-06-18",
  "source": "meeting-summary",
  "title": "Agent Skills Migration Sync",
  "summary": "The group agreed to export Prism skill and workflow references before creating published skills.",
  "participants": ["Contributor A", "Contributor B"],
  "links": [
    {
      "label": "Request #227",
      "url": "https://github.com/raid-guild/agent-skills/issues/1"
    }
  ],
  "signals": [
    {
      "kind": "decision",
      "text": "Keep skills/ empty until boundaries and validation paths are clear."
    },
    {
      "kind": "next_action",
      "text": "Review exported Prism references for durable capability groupings."
    }
  ]
}
```

## Portal Mapping

```json
{
  "activityItems": [
    {
      "title": "Prism reference export approved",
      "summary": "The team agreed to export Prism skill and workflow references before creating published skills.",
      "occurredAt": "2026-06-18",
      "sourceUrl": "https://github.com/raid-guild/agent-skills/issues/1"
    }
  ],
  "threads": [
    {
      "title": "Agent skills migration",
      "summary": "Ongoing work to refactor Prism skills into durable RaidGuild capability skills.",
      "status": "active"
    }
  ],
  "projects": [
    {
      "title": "RaidGuild Agent Skills",
      "summary": "Repository for reusable RaidGuild agent skills and migration references.",
      "status": "active",
      "links": [
        {
          "label": "Repository",
          "url": "https://github.com/raid-guild/agent-skills"
        }
      ]
    }
  ],
  "dailyBriefs": [
    {
      "date": "2026-06-18",
      "summary": "Agent skill migration moved forward with Prism reference export work.",
      "sections": [
        {
          "title": "Decision",
          "items": [
            "Keep skills/ empty until reusable capability boundaries are clear."
          ]
        },
        {
          "title": "Next Action",
          "items": [
            "Review exported references for migration groupings and validation paths."
          ]
        }
      ]
    }
  ]
}
```

## Mapping Guidance

- Map specific dated facts to `activityItems`.
- Map continuing efforts to `threads`.
- Map concrete collaboration surfaces to `projects`.
- Map summaries of current state to `dailyBriefs`.
- Use `wikiPages` for durable topic knowledge only when there are enough sources to support an evergreen page.
- Leave fields blank or draft-only when the source material does not support them.
