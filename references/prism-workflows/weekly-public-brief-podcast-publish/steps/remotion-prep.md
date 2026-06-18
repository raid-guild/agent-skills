# Remotion Prep

## Outcome

Produce the canonical Remotion payload and a render plan artifact for the latest approved audio set.

## Use This Context

- `tts-manifest.json`
- segment MP3 artifacts
- any explicit scene / composition requirements from the latest human feedback

## Durable Artifacts

Always write or refresh:
- `remotion-input.json`
- `render-plan.json`

The render plan should include at least:
- input artifact id
- output key
- composition id
- segment count
- scene fingerprint or version marker when available
- whether this payload supersedes a prior render input

## Rules

- do not leave the canonical payload only in chat text
- use absolute fetchable audio URLs when the scene expects remote audio
- keep payload shape deterministic
- if the human explicitly requests a new scene version, ensure the new payload is marked as superseding the older one
