Create a plural topic map before research/drafting. This step decides whether the request should become one wikiPage or several related wikiPages.

Required output artifact: wiki-topic-map.json or wiki-topic-map.md with:
- originalPromptTopic
- atomicTopicCandidates[] with title, neutral scope, why it is independent, source anchors, related candidates, likely Portal slug
- mergeOrSplitDecision: one-page | multi-page | needs-human-choice
- recommendedPrimaryPages[]
- deferredPages[]
- disallowedBlends[] explaining compound titles that should not be used

Rules:
- A title like "Personal CRM and Context Systems" should usually split into "Personal CRM" and "Context Systems" unless a verified existing term combines them.
- Avoid essay-style synthesis titles. Prefer noun-phrase encyclopedia titles.
- If more than one strong page exists, the workflow should produce a page set plan and either draft multiple pages or create follow-up requests for each page.
- Ask for human choice only when the split materially changes scope or publication intent.
