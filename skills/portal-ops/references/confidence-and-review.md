# Confidence And Review

Use this to decide create/update/draft/publish behavior.

## Confidence

- `publish`: source is clear, factual, dated, public-safe, and non-sensitive.
- `draft`: source is plausible but incomplete, ambiguous, sensitive, or needs human wording.
- `skip`: source is generic, duplicative, speculative, private, or not useful to the Portal.

Never publish:

- inferred commitments
- invented quotes
- private contact details
- task assignments not explicitly stated
- token/payment claims without source support
- client details without approval

## Create vs Update

Update existing records when the source continues a known storyline:

- same project spike
- same thread/topic
- same upcoming session
- same contributor profile
- same daily brief date/focus

Create new records when source introduces a distinct real object:

- new project with collaboration surface
- new recurring thread
- new dated activity item
- new scheduled session
- new durable wiki topic
- new reviewed post

## Output Shape

Return this shape unless the user requests direct edits:

```text
Source summary:

Proposed creates:
- collection:
  confidence:
  fields:
  source:

Proposed updates:
- collection:
  record:
  confidence:
  changes:
  source:

Skipped:
- item:
  reason:

Review notes:
```

## Guardrails

- Keep activity dated and source-grounded.
- Keep projects as collaboration surfaces.
- Keep threads lightweight.
- Keep sessions practical: title, time, join link, calendar/Discord links, related projects/threads, artifacts, and resources.
- Use direct human wording. Avoid generic AI summaries.
