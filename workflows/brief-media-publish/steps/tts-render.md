# TTS Render

Use `rg-media-render-ops` and `s3-object-storage`.

Read the approved `media-script.md`. Generate or prepare audio according to the configured TTS provider and approved voice mapping.

Upload generated audio files through `s3-object-storage` when render inputs require fetchable URLs.

Produce `tts-result.md` with:

- generated audio files
- uploaded object keys and fetchable URLs
- voice mapping
- duration, if available
- failures or retry notes

Do not use service-token-only artifact URLs as Remotion render inputs.
