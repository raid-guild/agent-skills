Draft or update one or more Portal wikiPages strictly from the wiki-data-model artifact. Do not invent structure directly in prose.

Required style:
- Wikipedia/reference page feel: neutral lead, clear hierarchy, explanatory paragraphs, source-backed claims, internal related-topic links where possible.
- Avoid opinion-piece language, aphorisms, punchy single-line paragraphs, and article framing.
- Do not make the fireside/session the subject unless the page is explicitly a session page.

Recommended sections: Lead, Background, Current state, Key concepts, Security/coordination implications, Tools and methods, Research and references, Open questions, Related topics, Further reading. Adapt section names to the topic.

Portal field mapping:
- body: rendered reference article
- keyClaims: claimLedger highlights
- furtherReading/papers/tools/openQuestions/prompts/relatedTopics/sourceArtifacts: populated from wiki-data-model

If topic-map selected multiple pages, either draft a coordinated page set or produce explicit follow-up change requests for deferred pages.

Body content rule:
- Do not put workflow metadata into the wiki page body. No visible lines like `Status: generated draft for review`, `Confidence: medium`, `Last researched:`, `Review notes:`, artifact ids, workflow step names, or internal review state.
- Store reviewStatus, confidence, lastReviewedAt/lastRefreshedAt, generatedAt, promptVersion, sourceArtifacts, and other operational metadata only in structured Portal fields or request artifacts.
- The rendered body should start with reader-facing topic content, not process metadata.
