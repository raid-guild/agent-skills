# Review

## Outcome

Wait for a human editorial decision on the weekly public summary and script before media generation.

## Decision Handling

Interpret the latest human gate instruction narrowly:
- explicit approve / approved / proceed -> route `approved`
- explicit changes requested / revise -> route `changesRequested`
- explicit reject / rejected / stop -> route `rejected`
- anything else -> do not invent a decision

## Review Checklist

A reviewer should confirm:
- the weekly summary is public-safe and accurate
- the brief gives a small but engaging peek into guild operations
- the output makes RaidGuild feel active and dynamic without exposing too much detail
- no client information, private strategy, or sensitive participant context leaked through
- the CTA appropriately points readers toward the Portal for deeper follow-through
- the workflow should proceed into TTS and video generation
