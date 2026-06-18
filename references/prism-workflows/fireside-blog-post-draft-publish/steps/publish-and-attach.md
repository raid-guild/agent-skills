# Publish And Attach

Use portal-ops-skill to create or update the Portal post and attach it to the originating session and/or wikiPage when applicable.

Before publishing, verify:
- approved draft exists
- generated header image artifact or approved visual fallback exists
- optional inline SVG charts/diagrams have been reviewed and are safe to embed
- source links are preserved
- metadata and tags are appropriate for the Portal blog destination

Create `publish-receipt.json` with Portal post id/slug/url, attached source objects, header image artifact used, optional inline SVG artifacts/snippets used, and publish status.
