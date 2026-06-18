Attach the completed recap package back to the Portal session/event and request.

Read session-source-pack.json, recap-plan.json, youtube-description.md, remotion-input.json, render-receipt.json.

Use portal-ops-skill / Payload API patterns to add or update Portal event/session resources for:
- Recap video output URL
- YouTube description draft
- Five-highlight recap plan
- Remotion render envelope / receipt

Do not publish to YouTube automatically. This workflow only creates the YouTube description draft and makes the video/resource package available for human use.

Create publish-receipt.json with Portal event id/url, added resource ids/labels/URLs, render output URL, YouTube description artifact, and verification. Add/refresh external refs for the Portal event and render output when supported.

If Portal attachment fails, create publish-blocker.md with the exact API error and do not close as success.
