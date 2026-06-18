# Load Campaign State

Load or create the campaign state for the Portal launch campaign.

Use the request description, comments, artifacts, and prior campaign request artifacts when available. If no prior state is available, use this default:

```json
{
  "campaign": "portal-launch-2026-06-03",
  "status": "active",
  "currentIndex": 0,
  "posts": [
    "problem",
    "mission",
    "portal-tease",
    "launch",
    "agent-first",
    "closing"
  ],
  "lastTweetId": null,
  "lastPostedAt": null
}
```

Resolve:
- current phase: `tease | problem | mission | launch | followup`
- current post index
- last posted at
- last X tweet id/url
- CMS link availability
- media status

Create or update `campaign-state.json` as a request artifact. Return the selected campaign post slot and what should happen next.
