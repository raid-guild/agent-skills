# TTS Render

## Outcome

Generate durable audio artifacts and a canonical manifest for all spoken segments.

## Voice Contract

Use Venice AI speech generation with:
- model: `tts-kokoro`
- response format: `mp3`
- streaming: `false`
- speed: `1.08`

Use fixed host voices by default:
- Queen Raida -> `af_heart`
- The Jester -> `am_michael`

If the latest human feedback explicitly overrides voices, follow the human override and record it in the manifest.

## Use This Context

- `podcast-script.json`
- any approved human override for host voice/persona settings

## Durable Artifacts

Write:
- one MP3 artifact per segment
- `tts-manifest.json`

The manifest must include, for every segment:
- order
- speaker
- artifact id
- filename
- voice
- model
- speed
- durationMs when available

## Rules

- fail loudly if any segment audio is missing
- do not rely only on local temp paths
- later steps should be able to reconstruct the render payload from the manifest alone
- record the actual Venice request settings used so later debugging does not guess at voice or speed assumptions
