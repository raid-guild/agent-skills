# Generate Media

Create a matching Queen Raida / Portal visual for the current X draft.

Read `campaign-state.json` and `x-draft.md`. Create `media-plan.md` with:
- visual concept
- image generation prompt
- negative prompt / avoidance notes
- alt text
- intended X attachment usage

Use image generation to produce one media candidate when available. Save the generated image as a request artifact when possible. If direct image artifact storage is unavailable, save `media-artifact-manifest.json` with generated file path, prompt, and placement notes.

Return the media artifact or manifest name.
