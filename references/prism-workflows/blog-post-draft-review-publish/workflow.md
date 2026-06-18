# Blog Post Draft Review Publish

This workflow handles blog-post requests that move through intake, drafting, media planning, image generation, human review, revision when needed, publish preparation, and Payload CMS draft publishing.

## Purpose

Use this workflow when a user wants a blog post drafted from Prism Memory and Prism Knowledge context, with image artifacts planned and generated before human review, and a final draft written into Payload CMS for admin review.

## Human Gate Behavior

The review step is the required human gate.

- approved -> publish-prep
- changesRequested -> revise
- rejected -> closed

The revise -> review loop may repeat until the reviewer approves or rejects the post.

## Durable State

Workflow runtime state belongs in DB-backed request/workflow records, not markdown files. Drafts, media plans, image prompt docs, generated images, and Payload publish receipts should be saved as request artifacts.

## Payload CMS Destination

This workflow expects a Payload CMS instance at the configured base URL and publishes posts as drafts, not as public published content.

## Image Durability And Publish Rules

Generated blog images should be saved as direct request image artifacts whenever the runtime path supports it. A manifest-only record is a fallback, not the preferred success path.

When a publish package selects inline images for use in the article body, the publish step must embed those images into the CMS post content, not only upload them to the media library. Uploading inline media without placing it in the post body should be treated as incomplete publish behavior and called out explicitly in the publish receipt.

## SEO Guardrails

Publish-prep and publish should treat the CMS SEO checks as part of the workflow contract, not optional polish.

Default targets:
- meta title: 50-60 characters
- meta description: 100-150 characters
- meta image: present and relevant

When the strongest editorial title is too long for the SEO field, keep a readable on-page headline but also provide a CMS-safe meta title variant that passes the check.
