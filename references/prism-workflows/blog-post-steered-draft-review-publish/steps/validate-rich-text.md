# Validate Rich Text

Outcome: verify and normalize the Payload CMS post rich text before publishing, so the Payload editor does not throw Lexical runtime errors.

Use PAYLOAD_CMS_BASE_URL, PAYLOAD_CMS_EMAIL, and PAYLOAD_CMS_PASSWORD. Authenticate with POST /api/users/login and Authorization: JWT <token>.

Find the CMS post created or updated by publish-prep from request external refs, publish-prep artifacts, or the prior step summary. If no CMS post id can be identified, stop and report that validation cannot proceed; do not publish.

Fetch the post with /api/posts/{id}?depth=0&draft=true. Inspect the rich-text field `content.root`. Normalize the Lexical tree before publish:

- Every `list` node must include `direction`; use `ltr` when missing.
- For bullet lists (`type: list`, `tag: ul`, or `listType: bullet`), every direct `listitem` child must have `value: 1`. Do not number bullet list items as 1, 2, 3.
- For ordered lists, list item values may be sequential.
- List items should contain valid block children such as paragraphs or nested lists, not raw text nodes directly. Wrap raw text children in paragraphs if found.
- Remove unsupported/extra paragraph fields inside list items when they differ from known-good Payload Lexical output; in particular, remove `textStyle` from paragraphs nested under list items and keep `textFormat`.
- Preserve the article text, headings, links, metadata, visibility, status, authors, and all non-content fields.

If normalization changed the tree, PATCH /api/posts/{id}?depth=0&draft=true with the corrected `content` and existing status. Fetch it again and verify no bullet list items have values other than 1 and no list nodes are missing direction.

Save a durable artifact named `lexical-validation-report.json` with post id, fields checked, changes made, and remaining issues. Continue to publish only when remaining issues is empty.
