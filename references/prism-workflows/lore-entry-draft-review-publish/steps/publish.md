# Publish

Publish the approved lore entry package to Payload CMS as a draft unless the request explicitly says to publish live.

Use `publish-package.json` or `publish-package.md`. Ensure:
- tag `lore` is present
- selected image is uploaded/attached as featured or inline media where possible
- post status is draft by default
- title, excerpt, SEO fields, and body match the approved package

Create `publish-receipt.md` with the CMS response, draft URL/admin URL when available, selected tags, image handling result, and any incomplete publish behavior.

Return the publish receipt artifact and CMS draft link if available.
