# Publish

Publish the approved content into Payload CMS as a draft post.

## Required Environment

- PAYLOAD_CMS_BASE_URL
- PAYLOAD_CMS_EMAIL
- PAYLOAD_CMS_PASSWORD

Optional environment:

- PAYLOAD_CMS_POSTS_PATH (default /api/posts)
- PAYLOAD_CMS_MEDIA_PATH (default /api/media)
- PAYLOAD_CMS_USERS_LOGIN_PATH (default /api/users/login)
- PAYLOAD_CMS_DEFAULT_STATUS (default draft)

## Inputs

Use the latest publish-prep artifact plus any selected image artifacts.

## Behavior

1. Log in to Payload CMS and get a JWT.
2. Upload the chosen hero and inline image artifacts to the media collection when they are present.
3. Convert the prepared blog content into the Payload post payload shape expected by the destination, including Lexical content structure.
4. Set the chosen hero image on the post metadata.
5. Apply the prepared SEO fields from publish-prep:
   - use `metaTitle` when provided, otherwise only use the main title if it still fits the target range
   - use `metaDescription` from publish-prep rather than a raw long excerpt
6. If inline images were selected in publish-prep, embed them into the Lexical post body at their specified placement hints.
7. Create the post as a draft with _status set to draft unless explicitly configured otherwise.
8. Save a publish receipt as a request artifact containing at least the created Payload post id, slug, media ids, admin URL, whether inline images were embedded, and the final SEO field values used.

## SEO rule

Do not treat failing obvious CMS SEO length checks as acceptable default output. If the prepared SEO title or description misses the expected range, revise them before publish and record the final values used.

## Inline image rule

Uploading inline images to the CMS media library is not enough. If publish-prep selected inline images for article-body use, the publish step should embed them into the post content.

If inline images were selected but the runtime cannot embed them into the Lexical body, return a clear partial or blocked result and record that mismatch in the publish receipt instead of silently publishing a hero-only result as if inline placement succeeded.

## Output

Return a concise publish summary with:

- post id
- slug
- draft status
- uploaded media ids
- which image was used as hero
- which inline images were embedded in-body
- final meta title
- final meta description
- admin URL when available

If Payload credentials or content conversion are unavailable, return a clear blocked result rather than partially publishing.
