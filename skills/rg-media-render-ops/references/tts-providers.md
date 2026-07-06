# TTS Providers

Use this when a media workflow needs generated narration, podcast audio, or recap voice segments.

## Provider Boundary

`rg-media-render-ops` should not hard-code one commercial TTS provider as a universal requirement. It owns the render-facing audio contract:

- which script segment maps to which speaker
- which provider/model/voice produced each file
- where the generated file is stored
- whether the renderer can fetch the audio URL
- duration and retry metadata

Provider-specific clients, credentials, and API calls belong to the active workflow environment.

## Current Prism Default

Historical Prism brief/podcast workflows used Venice AI speech generation with Kokoro:

- provider: `venice`
- model: `tts-kokoro`
- default Queen Raida voice: `af_heart`
- default Jester voice: `am_michael`

Use those defaults when a workflow asks for the established RaidGuild/Prism podcast setup and no newer approved provider mapping is present.

## Provider Selection

Follow this order:

1. Use the provider and voice mapping explicitly approved in the workflow request or human gate.
2. Use workflow-local configuration if present.
3. Use the current Prism default above for existing brief/podcast flows.
4. If no provider is configured, stop with a concrete missing-provider blocker instead of inventing a TTS route.

Do not assume ElevenLabs/11Labs unless the workflow, environment, or operator explicitly names it.

## Manifest Fields

Record enough detail that a later render failure can be debugged without guessing:

- provider
- model
- voice
- speed or other generation settings
- source script segment id
- output artifact path
- uploaded object key
- fetchable URL
- durationMs
- retry/failure notes
