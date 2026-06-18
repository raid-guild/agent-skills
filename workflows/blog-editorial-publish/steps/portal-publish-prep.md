# Portal Publish Prep

Use `rg-portal-ops`.

Create `publish-package.json`.

Include:

- title
- slug
- excerpt/dek
- body content
- source links
- tags
- category recommendation
- visibility
- draft vs publish expectation
- selected hero image and inline image placements
- alt text
- SEO title and description
- reviewer notes

Rules:

- Prepare for Portal without writing unless this step is explicitly configured to create a draft.
- Default to draft unless the operator or workflow explicitly requests live publish.
- Use `rg-public-output-safety` result as part of the package.
- Do not silently drop selected inline images; either embed them or record the limitation.
