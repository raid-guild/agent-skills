# Output JSON Contract

Return exactly this JSON shape and no extra prose:

```json
{
  "sanitizedText": "",
  "changes": [
    {
      "type": "redaction | rewrite | removal | softening | link_replacement | persona_fix | none",
      "before": "",
      "after": "",
      "reason": ""
    }
  ],
  "blockers": [
    {
      "type": "secret | internal_url | local_path | private_ops | unsupported_claim | confusing_debug_language | persona_mismatch | needs_source | needs_approval | human_review",
      "severity": "low | medium | high | critical",
      "reason": "",
      "suggestedResolution": ""
    }
  ]
}
```

If no changes are needed, return the original draft in `sanitizedText`, `changes` as an empty array, and `blockers` as an empty array.

Severity guidance:

- `low`: safe to publish after minor cleanup.
- `medium`: likely safe after edits or source clarification.
- `high`: do not publish until resolved.
- `critical`: contains secrets, private information, or dangerous approval gaps; do not publish.
