# Review

## Outcome

Wait for a human editorial decision on the written brief and script before media generation.

## Decision Handling

Interpret the latest human gate instruction narrowly:
- explicit approve / approved / proceed -> route `approved`
- explicit changes requested / revise -> route `changesRequested`
- explicit reject / rejected / stop -> route `rejected`
- anything else -> do not invent a decision

## Review Checklist

A reviewer should confirm:
- the internal brief is useful and accurate
- the chosen date window makes sense
- the script is suitable for internal members
- the workflow should proceed into TTS and video generation
