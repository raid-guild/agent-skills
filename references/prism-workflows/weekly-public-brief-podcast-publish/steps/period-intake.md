# Period Intake

## Outcome

Resolve the weekly period, source set, audience, and public-safety constraints for the run.

## Use This Context

- request title and description
- latest request comments
- linked artifacts or external refs
- Prism Memory and digest context for the target week

Use `prism-api-reader` when retrieval is needed.

## Required Output

Return:
- resolved weekly date range
- shortlist of source artifacts / docs
- public-safety constraints and exclusions
- clear recommendation to proceed or pause for human input

## Durable Artifacts

If the resolved scope materially differs from the request text, write a concise intake summary artifact.

## Rules

- prefer exact dates over vague ranges
- explicitly call out uncertainty
- do not infer private-safe content as public-safe without saying so
