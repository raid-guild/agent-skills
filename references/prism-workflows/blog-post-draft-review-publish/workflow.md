# Blog Post Draft Review Publish

This workflow handles intake, optimization planning, drafting, media, human review, revision, publish preparation, and Payload CMS draft creation.

## Purpose

Create source-grounded blog posts optimized for search engines, answer engines, and generative retrieval, with durable media and publishing evidence.

## Content Quality Sequence

Use `rg-content-strategy` during intake and drafting, `rg-scribe-publisher-skill` plus `rg-brand-voice` during drafting and revision, and `rg-public-output-safety` during publish preparation. Safety review is mandatory before any CMS mutation. Unresolved blockers route to `needs-attention`; only a passing `safety-result.json` may continue to publish.

## Human Gate

The review step is required: approved advances to publish prep, changesRequested returns to revise, and rejected closes the request.

## Durable State

Save the optimization brief, drafts, media plans, images, safety result, publish package, CMS receipt, and validation reports as request artifacts. Runtime state remains DB-backed.

## SEO, GEO, And AEO Contract

Intake defines the primary query, audience question, named entities, likely follow-up questions, and internal-link candidates.

Drafting must answer the audience question directly near the opening, use question-led headings when useful, preserve source notes, and distinguish firsthand findings from sourced claims.

Publish preparation must verify:

- meta title: 50-60 characters
- meta description: 100-150 characters
- canonical URL
- named author
- article-specific social image
- descriptive image alt text
- relevant internal links
- valid Article JSON-LD
- FAQ JSON-LD only for genuine FAQ content

Keep a readable editorial headline and a shorter meta title when needed.

## CMS Order

Publish prep performs the mandatory safety check and creates the package, publish creates or updates a Payload draft, and rich-text validation checks both Lexical content and SEO/GEO/AEO evidence before human verification.
