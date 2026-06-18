Build the structured data model that the draft must render from. Do not write prose-first.

Required output artifact per candidate page:
- leadDefinition
- scopeIn / scopeOut
- sectionHierarchy
- claimLedger[]: claim, sourceIds, confidence, status verified|inferred|open, notes
- sourceLedger[]: id, title, url, publisher/sourceType, datePublished if known, dateAccessed, relevance
- terms[]
- timeline[] where useful
- tools[]
- papers[]
- furtherReading[]
- openQuestions[]
- relatedTopics[]
- sourceSessionAnchors[]
- draftingConstraints[]

Quality bar:
- The page must feel like a Wikipedia/reference page: neutral lead, stable section hierarchy, sourced claims, no punchy thesis lines, no excessive one-line paragraphs.
- Session material should appear as source context, not as the main frame, unless the wikiPage is explicitly about the session.
- If the data model is thin, return needs-human-input or source-research-needed instead of drafting.
