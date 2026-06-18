# Notify Discord

Post a concise Discord summary only after publish and state advancement.

Use the configured Discord destination if one is attached to the request/task output configuration. Include:
- text used
- image artifact or media status
- tweet URL
- next scheduled post/phase

Do not include internal URLs, tokens, raw API output, local paths, or workflow debug details. Create `discord-summary.md` with the summary that was or should be sent.

Return the Discord summary and delivery status.
