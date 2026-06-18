# Page Copy

Use `PageCopy` for copy edits to fixed Portal product-flow pages. Do not hardcode copy changes in React components when the page is already CMS-managed.

## Managed Routes

- `/join` -> `PageCopy.key = "join"`
- `/inquire/client` -> `PageCopy.key = "inquire-client"`
- `/inquire/sponsor` -> `PageCopy.key = "inquire-sponsor"`
- `/inquire/grant` -> `PageCopy.key = "inquire-grant"`
- `/inquire/opportunity` -> `PageCopy.key = "inquire-opportunity"`
- `/inquire/general` -> `PageCopy.key = "inquire-general"`

## Fields

Use `PageCopy` fields for:

- eyebrow
- headline
- intro
- context heading/body
- CTA labels
- post-submit copy
- SEO title/description
- join-page benefit bullets
- join-page funnel links

## Rules

- Treat page copy updates as human-reviewable unless explicitly approved.
- Only admins/editors should manage `PageCopy`.
- Do not create a new collection for copy-only intake changes.
- Keep form submissions writing to `inquiries`.
- Keep inquiry page routes tied to existing inquiry types unless a new intake lane is explicitly requested.

Existing inquiry types:

- `client`
- `sponsor`
- `grant`
- `opportunity`
- `general`

For a new consultation-style MVP, prefer a `client` inquiry variant with source-route or intent tracking before adding a new type.
