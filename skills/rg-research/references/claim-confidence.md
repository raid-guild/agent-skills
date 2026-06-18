# Claim Confidence

Use confidence labels to keep research output honest.

## Labels

- `verified`: direct support from a primary source or multiple reliable independent sources.
- `likely`: good support, but missing one primary detail or current confirmation.
- `uncertain`: partial, stale, indirect, or conflicting support.
- `unsupported`: no reliable source found.
- `contradicted`: reliable source conflicts with the claim.
- `private-only`: supported only by private/internal material; not public-safe without approval.

## Verification Rules

- For current facts, verify with a recent source.
- For product/API/library behavior, prefer official docs, source code, changelogs, or release notes.
- For company/person facts, verify live because they can change.
- For public content, cite public sources where possible.
- For internal RaidGuild context, separate what can be said publicly from what is only useful internally.

## Claim Check Output

```json
{
  "claim": "",
  "verdict": "verified | likely | uncertain | unsupported | contradicted | private-only",
  "confidence": "high | medium | low",
  "supportingSources": [],
  "contradictingSources": [],
  "notes": ""
}
```
