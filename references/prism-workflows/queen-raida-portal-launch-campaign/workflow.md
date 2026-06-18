# Queen Raida Portal Launch Campaign

This workflow runs an autonomous Queen Raida campaign for the RaidGuild Portal launch. It creates one X post at a time, generates matching media, sanitizes public output, publishes to X only when sanitizer checks pass, advances campaign state, and sends a Discord summary.

## Purpose

Use this workflow for the Portal launch campaign arc, especially around the planned 2026-06-03 launch. The campaign should feel like Queen Raida: clear, useful, public-safe, and lightly operational-occult. It should not expose internal URLs, workflow debug details, private Discord content, or unsupported launch claims.

## Campaign State

Default state shape:

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

The workflow should persist campaign state as `campaign-state.json` on each request. New scheduled runs should try to find the latest campaign state from previous Portal campaign requests/artifacts before falling back to the default state.

## Autonomous Publishing

There is no human gate in this workflow. The sanitizer step is the control point. High or critical sanitizer blockers must stop the run before X publishing. The publish step must verify the configured X account is @raidguildish, verify the final post is 280 characters or fewer, and must not publish unsupported launch claims, internal URLs, private operational details, or confusing workflow/debug language.

## Artifacts

Expected durable artifacts:
- `campaign-state.json`
- `x-draft.md`
- `media-plan.md`
- generated image artifact or `media-artifact-manifest.json`
- `sanitized-output.json`
- `publish-receipt.json`
- `discord-summary.md`

## Publishing Safety

Use Queen Raida source docs and public-safe Portal facts. Before publishing, run the public sanitizer. Do not post unreviewed drafts. Do not call X if the final post is over 280 characters; trim first and record the final character count. Do not claim the Portal is live unless the request context includes a public CMS or launch URL confirming it.
