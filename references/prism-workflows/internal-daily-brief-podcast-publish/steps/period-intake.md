# Period Intake

## Outcome

Resolve the date window, source set, audience, and internal handling constraints for this run.

## Use This Context

- request title and description
- latest request comments
- linked artifacts or external refs
- Prism Memory and digest context for the candidate day or days

Use `prism-api-reader` when retrieval is needed.

## Date Window Rules

Start with the latest single UTC day in scope.

If that day is too sparse, expand backward up to a few days until the brief has enough material to be useful.

Treat "enough material" pragmatically. Prefer a compact multi-day internal brief over a low-signal single-day brief.

## Durable Artifacts

Write `brief-window.json` with:
- chosen start date
- chosen end date
- whether the window was expanded
- short rationale
- key source artifacts or digests used

## Required Output

Return:
- resolved date window
- shortlist of source artifacts / docs
- internal audience constraints
- clear recommendation to proceed or pause for human input
