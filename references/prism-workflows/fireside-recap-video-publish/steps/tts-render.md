Generate one MP3 narration segment for each FiresideRecapScene audio slot where possible: intro, each of the 5 cards, and outro.

Read recap-plan.json.

Use the same TTS approach as the weekly podcast workflows when environment/API support is present. Prefer MP3, non-streaming, and stable voices appropriate for a concise recap.

For each segment:
- Generate an MP3 artifact.
- Probe or calculate actual durationMs.
- Add roughly 700-1200ms visual tail for the Remotion durationMs field.

Create tts-manifest.json with:
- intro: script, artifact id/path, durationMs, measuredAudioDurationMs
- cards[5]: title, script, artifact id/path, durationMs, measuredAudioDurationMs
- outro: script, artifact id/path, durationMs, measuredAudioDurationMs
- TTS provider/settings/voice metadata

If TTS is unavailable, create tts-blocker.md with the exact missing env/API condition and stop. Do not proceed to remotion-prep without MP3 artifacts or explicitly approved audio-less fallback.
