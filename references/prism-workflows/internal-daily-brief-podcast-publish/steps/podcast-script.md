# Podcast Script

## Outcome

Generate the two-host script and structured segment data needed for TTS.

## Host Pattern

Use a fixed two-host pattern:
- Queen Raida: main female host, clear lead voice
- The Jester: color / humor, but still grounded and concise

Do not invent a third narrator.

## Durable Artifacts

Write both:
- `podcast-script.md`
- `podcast-script.json`

The JSON artifact should include ordered segments with:
- speaker
- text
- intended voice
- approximate purpose of the segment

## Rules

- keep the script suitable for internal publication
- make segment ordering deterministic
- preserve operational context without turning the script into a raw transcript dump
- keep The Jester useful; light color is fine, but do not derail the brief with filler jokes
- set intended voices explicitly as `af_heart` for Queen Raida and `am_michael` for The Jester unless a human overrides them
