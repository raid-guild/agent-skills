# Podcast Script

## Outcome

Generate the two-host script and structured segment data needed for TTS.

## Host Pattern

Use a fixed two-host pattern:
- Queen Raida: main female host, clear lead voice
- The Jester: color / humor, but still grounded and concise

Do not invent a third narrator.

## Use This Context

- latest weekly summary artifacts
- public audience constraints
- any reviewer guidance captured before this step

## Durable Artifacts

Write both:
- `podcast-script.md`
- `podcast-script.json`

The JSON artifact should include ordered segments with:
- speaker
- text
- intended voice
- approximate purpose of the segment

## Framing Rules

- keep the script fully publishable as written
- make segment ordering deterministic
- keep The Jester useful; light color is fine, but do not derail the brief with filler jokes
- set intended voices explicitly as `af_heart` for Queen Raida and `am_michael` for The Jester unless a human overrides them
- present the brief as a small, engaging peek into guild operations
- show visible activity, momentum, and project movement without drifting into private detail
- do not include client information, private strategy, or sensitive internal context

## CTA Rule

End the script with a concise public call to action that directs listeners to join or follow the Portal to get more detail, follow along, see active projects, join upcoming sessions, and plug into real opportunities across RaidGuild.
