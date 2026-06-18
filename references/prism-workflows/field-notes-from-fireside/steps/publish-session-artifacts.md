Publish generated artifacts to the Portal session/event resources only. Do not create, update, draft, or publish any Portal post. Do not create or update Portal wiki pages.

Required behavior:
- Use portal-ops-skill and authenticated Payload CMS API access to update the Portal event/session resources.
- Read the current Portal event by id and preserve existing events.resources entries.
- Attach available session source resources: recording, transcript, summary, source artifact.
- Attach generated planning artifacts when present: source-pack.md, angle-plan.md / topic-angle-map.md, topic-map.md, media-brief.md / media-plan.md, routing-plan.md, and publish/verification packets.
- Request artifacts from the change-board API are service-token protected and must not be linked directly from Portal resources.
- For protected generated markdown artifacts, mirror each generated artifact into Prism Memory with source: "prism-workflow", type: "workflow_artifact", bucket: "portal", and metadata containing request_number, portal_event_id, request_artifact_id, request_artifact_name, and workflow_key.
- Use the returned human-viewable Prism artifact URL as the Portal event resource URL.
- Use resourceType: "artifact" for artifact URLs and stable labels such as "Source pack", "Topic map", "Angle brief", "Media plan", "Routing plan", "Session transcript", and "Session summary".
- Avoid duplicate resources with the same URL.
- After PATCH /api/events/:id, re-read the event and verify expected resource URLs are present.

Strict prohibition:
- Do not POST/PATCH /api/posts.
- Do not create a Portal post draft.
- Do not write article/blog prose in this step.
- Do not publish public copy.

Output:
- Create a request artifact named portal-event-artifacts-verification.json listing event id, resource labels, URLs, resourceType values, mirrored Prism artifact ids if any, and any failures.
- Return a concise summary of resources attached and any resources skipped.
