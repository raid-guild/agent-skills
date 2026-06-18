# Publish

## Outcome

Publish the approved internal brief and save a durable receipt of what was written.

Use `portal-memory-publisher` guidance for Portal CMS field assumptions.

## Preconditions

Before publishing, verify the domain evidence:
- there was an explicit publish approval
- the chosen `render-receipt.json` has `finalStatus: completed`
- the chosen media URL is explicit in the receipt
- if publishing a fallback receipt instead of the newest rerun, that fact is stated in the publish receipt

## Portal CMS Rules

Do not send `visibility: internal`.

Use Portal CMS visibility vocabulary:
- `public`
- `authenticated`
- `admin`

For this workflow, member-only briefs should default to `visibility: authenticated` unless the live Portal collection config proves a different value is required.

Treat a Payload 4xx validation response as a schema/value problem, not a reason to rerun remotion or TTS.

## Durable Artifacts

Write `publish-receipt.json` with at least:
- chosen render receipt id
- chosen media URL
- target record id
- final CMS status
- exact visibility sent to the CMS
- timestamp
- any fallback / override rationale

## External Refs

Attach an external ref for the live internal record when a stable target URL or record identity exists.

## Notes

This step should describe what was published and what evidence proves it. The published record should be member-visible through the Portal CMS, not public.
