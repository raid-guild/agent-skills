Resolve the exact completed Portal fireside session to recap.

Inputs may include a Portal event/session URL, Portal event id, request references, transcript artifact, summary artifact, or parent field-notes artifacts.

Required behavior:
- Use portal-ops-skill / Payload API patterns to inspect the Portal session/event and its attached resources.
- Use Prism read APIs for linked artifacts when the session references Prism artifact URLs.
- Confirm the session is completed or has enough final transcript/summary material to recap.
- Collect canonical sources: Portal event URL/id/title/date, guest/host names and handles if available, transcript artifact, summary artifact, source pack, angle/topic map, media brief, and any existing image/avatar/background resources.
- Do not invent guest handles or avatar URLs. If missing, record a needs-human-input note or use a clearly documented configured/default asset only when the workflow/request allows it.

Create session-source-pack.json with:
- portalEventId, portalEventUrl, eventTitle, eventDate, guest, host
- all attached artifact/resource URLs and ids
- source reliability notes
- missing fields / blockers
- recommended title/subtitle seed

If no completed session or usable transcript/summary exists, create intake-blocker.md and stop with a concise blocker summary. Otherwise recommend recap-plan.
