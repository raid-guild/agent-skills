# Publish

## Outcome

Publish the approved weekly brief and save a durable receipt of what was written.

## Preconditions

Before publishing, verify the domain evidence:
- there was an explicit publish approval
- the chosen `render-receipt.json` has `finalStatus: completed`
- the chosen media URL is explicit in the receipt
- if publishing a fallback receipt instead of the newest rerun, that fact is stated in the publish receipt

## Durable Artifacts

Write `publish-receipt.json` with at least:
- chosen render receipt id
- chosen media URL
- target record id
- final CMS status
- timestamp
- any fallback / override rationale

## External Refs

Attach an external ref for the live published record when a stable target URL or record identity exists.

## Notes

This step should describe what was published and what evidence proves it. Platform request status semantics are owned by the workflow engine.
