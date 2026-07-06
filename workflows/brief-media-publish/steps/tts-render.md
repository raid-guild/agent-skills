# TTS Render

Use `rg-media-render-ops` and `s3-object-storage`.

Read the approved `media-script.md`. Generate or prepare audio according to the configured TTS provider and approved voice mapping.

Use the current Prism default for existing brief/podcast flows when no newer mapping is approved: Venice AI with `tts-kokoro`, `af_heart` for Queen Raida, and `am_michael` for The Jester. Do not assume ElevenLabs/11Labs unless the workflow config or operator explicitly names it.

Upload generated audio files through `s3-object-storage` when render inputs require fetchable URLs.

Produce `tts-result.md` with:

- generated audio files
- provider, model, voice, and generation settings used
- uploaded object keys and fetchable URLs
- voice mapping
- duration, if available
- failures or retry notes

Do not use service-token-only artifact URLs as Remotion render inputs.
