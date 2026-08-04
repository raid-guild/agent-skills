# Publish Prep

Use `rg-public-output-safety` to review the exact approved public-facing post before preparing it for Payload. Save `safety-result.json` using the skill's required JSON contract.

If the safety result is blocked, has unresolved high or critical blockers, or lacks required human approval, do not prepare a publishable package and do not allow CMS mutation. Save `safety-blocker.md` and return `needsAttention` so the workflow routes to `needs-attention`.

Only after a passing safety result, prepare the approved post for publishing without mutating Payload. Return `completed` so the workflow continues to `publish`.

The output of this step should be suitable input for the Payload CMS publish step.

## SEO requirements

In addition to the editorial draft, prepare CMS-safe SEO fields that are expected to pass the current checks:

- `metaTitle`: target 50-60 characters
- `metaDescription`: target 100-150 characters
- `metaImage`: selected and relevant hero image

If the best on-page headline is longer than the SEO-safe range, keep both:
- an editorial post title for the article itself
- a shorter `metaTitle` variant for CMS SEO

Likewise, write a `metaDescription` that is concise enough to pass the range check instead of copying a long excerpt unchanged.

## Output contract

The publish package should include at least:
- article title
- optional seo title variant when different
- excerpt
- meta title
- meta description
- slug
- canonical URL
- named author
- tags
- markdown
- valid Article JSON-LD using verified title, description, author, image, dates, canonical URL, and publisher values
- FAQ JSON-LD only when the post contains genuine FAQ content; otherwise omit it
- selected hero image ref
- selected inline image refs with placement hints when applicable

Never invent author identities, dates, URLs, or structured-data values. Treat a missing canonical URL, named author, or valid Article JSON-LD as a blocker.

## Image selection rules

- Select one hero image when a hero image exists.
- Select inline images only when they are actually intended to appear inside the article body.
- For every selected inline image, include an explicit placement hint tied to a section or paragraph so the publish step can embed it into CMS content.
- If an inline image is uploaded only as optional media and should not appear in the body, mark it as not selected for embedding.
- Prefer direct request image artifact ids when available. Use manifest-backed fallback references only when direct image artifacts do not exist.
