# Hivemind Context

Use Hivemind as a strategy/context source, not as factual authority by itself.

Use it when the operator asks to consult Hivemind, search Hivemind knowledge, or use marketing/GTM/positioning context.

## Boundary

- Good for: positioning, GTM patterns, content strategy context, project/conversation context.
- Not enough for: current factual verification, legal/financial/medical claims, API behavior, or public claims that need citations.

## Credential Handling

Hivemind requires an API key for authenticated calls. Check for key presence only; never print, log, or persist key values.

Expected environment variables:

- `HIVE_MIND_API_KEY`
- `HIVEMIND_API_KEY`

## Research Handling

When using Hivemind:

1. State that a finding came from Hivemind context.
2. Preserve source titles/authors if returned.
3. Separate Hivemind synthesis from verified source facts.
4. Verify public claims through public sources before publishing.
