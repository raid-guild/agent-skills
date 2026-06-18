Use portal-ops-skill to create or update the Portal wikiPages collection, but follow these wiki-specific publish rules exactly.

Before any Portal CMS write:
- Fetch the canonical Portal ops skill from https://portal.raidguild.org/api/portal/skills/portal-ops-skill.
- Read SKILL.md and references/portal-cms-model.md from that payload.
- Authenticate to Payload with PAYLOAD_CMS_BASE_URL, PAYLOAD_CMS_EMAIL, and PAYLOAD_CMS_PASSWORD through POST /api/users/login.
- Use the returned JWT as Authorization: JWT <token> for Portal API writes. Do not use the Prism/site service token as Portal CMS auth.

Wiki publish rules:
- Published wiki pages must have reviewStatus: reviewed.
- If the review gate approved publication, convert the reviewed proposal to reviewStatus: reviewed and _status: published before writing.
- Never create or update an admin-only wiki page. If visibility is admin, block and ask for human direction.
- Use public/authenticated/member visibility only when source facts and audience are clear.
- If the page should remain exploratory or not yet reviewed, write a draft instead of publishing.

Schema normalization required before POST/PATCH /api/wikiPages:
- body must be valid Payload Lexical JSON, not raw Markdown.
- prompts entries require both label and prompt.
- papers/furtherReading entries require the live field names accepted by Portal; normalize before writing.
- sourceArtifacts must use valid sourceType values; omit invalid sourceArtifacts rather than failing the whole publish.
- Avoid custom Lexical list nodes unless they are known-valid for the deployed editor config.

Success requirements:
- Verify the public URL returns 200, preferably https://portal.raidguild.org/wiki/<slug>.
- Attach a Portal external ref with provider portal, kind wiki_page, collection wikiPages, id, slug, status, reviewStatus, and public URL.
- Save a publish-success artifact with the id, slug, public URL, reviewStatus, and _status.

Failure requirements:
- If authentication fails, Portal returns 403, validation fails, or the public URL cannot be verified, save publish-blocked.md with exact status/error and required handoff.
- The step must report failure/blockage clearly. Do not claim success, do not attach a published external ref, and do not allow the workflow to close as if a wiki page was published.

Return the wikiPage id/slug/public URL, source list, unresolved questions, and suggested mature blog topics only after the Portal record exists and the public URL is verified.

Body scrub before publishing:
- Before converting to Lexical and writing to Portal, remove any operational header lines from the body, including `Status:`, `Confidence:`, `Last researched:`, `Generated draft`, `Review notes:`, artifact ids, and workflow-step notes.
- If the draft still includes visible workflow metadata, clean it during publish and mention the cleanup in the publish-success artifact.
- Do not publish operational metadata as reader-facing wiki content.
