# Generate Image

Generate the blog header/feature visual. This step is required before review.

Read `blog-draft.md`, the source notes, and any request comments. Create `image-brief.md` with:
- visual concept
- image generation prompt
- negative prompt / avoidance notes
- alt text
- placement recommendation for the Portal post
- any optional inline SVG chart/diagram recommendations for the article body

Default header image art direction:
- mythic fireside / bonfire atmosphere
- wizards and warriors as the recurring visual cast
- warm firelight, ember glow, night gathering, practical fantasy gear
- RaidGuild-adjacent mood: builders, ritual, strategy, craft, fellowship
- cinematic editorial illustration, not cartoon mascot art
- grounded in the specific blog thesis, not generic fantasy wallpaper

Prompt requirements:
- Include wizards and warriors near a bonfire or fireside gathering unless the request explicitly says otherwise.
- Tie the scene to the post topic through symbols, setting, objects, or composition.
- Avoid readable text, logos, UI screenshots, distorted hands/faces, gore, modern stock-photo styling, and literal private/person-identifiable depictions.
- Keep the image suitable for a public Portal blog feature image.

Use the imagegen skill to generate one suitable raster header image. Save the generated image as a request artifact when possible. If direct image storage is unavailable, save `image-artifact-manifest.json` with the generated file path or provider reference, prompt, alt text, and usage notes.

Inline explanatory charts, maps, relationship diagrams, or process diagrams may be authored as inline SVG snippets when they clarify the article. Keep inline SVGs simple, accessible, and data/source-grounded. Do not use inline SVGs as a substitute for the required generated header image.

Do not skip this step silently. If imagegen is unavailable or fails, create `image-generation-blocker.md` explaining the failure and whether a text-only/placeholder fallback is acceptable for human review.

Return the header image artifact or blocker artifact name, plus any inline SVG recommendations or artifact names.
