# Fireside Blog Post Draft Publish

Create one focused RaidGuild Portal blog post from a narrow fireside session topic or a mature Portal wiki topic with a clear thesis.

This workflow is not a broad session recap and not a wiki inventory. It should produce a bounded essay, a generated visual, human review, and a Portal draft/published post with source attachments.

## Required Outputs

- `source-ledger.json` or equivalent source notes
- `blog-draft.md`
- `image-brief.md`
- generated header image artifact or `image-artifact-manifest.json`
- optional inline SVG chart/diagram snippets when useful
- `review-notes.md` when requested
- `publish-receipt.json`

## Visual Requirement

Every successful draft must pass through the image generation step before review. The visual step must create an image brief and attempt image generation using the `imagegen` skill for the Portal header/feature image. The default header visual language is mythic fireside: wizards and warriors gathered around or near a bonfire, cinematic but grounded in the post topic. Inline explanatory charts, maps, or diagrams inside the article may be authored as inline SVGs when useful; those do not replace the required header image. If image generation is unavailable, the step must create a blocker or explicit fallback manifest; it must not silently skip visuals.

## Source Discipline

Use Portal/session/wiki source material only as evidence for the selected topic. Do not invent facts, session claims, links, quotes, or project state. Surface uncertainty when source material is incomplete.

## Review

Human review decides whether the post is approved, needs revision, or should be closed. Review must check scope, factual support, public safety, and whether the visual artifact exists or has an explicit approved fallback.
