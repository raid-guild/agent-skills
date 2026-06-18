# Publish Prep

Prepare the approved post for publishing without actually publishing it. Return title, excerpt, tags, slug recommendation, markdown, and references to the selected image artifacts that should travel with the publish package.

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
- tags
- markdown
- selected hero image ref
- selected inline image refs with placement hints when applicable

## Image selection rules

- Select one hero image when a hero image exists.
- Select inline images only when they are actually intended to appear inside the article body.
- For every selected inline image, include an explicit placement hint tied to a section or paragraph so the publish step can embed it into CMS content.
- If an inline image is uploaded only as optional media and should not appear in the body, mark it as not selected for embedding.
- Prefer direct request image artifact ids when available. Use manifest-backed fallback references only when direct image artifacts do not exist.
