# Source Ledger

Use a source ledger whenever downstream work depends on factual grounding.

## Ledger Fields

- `sourceId`: short stable id.
- `title`: source title or artifact label.
- `url`: public URL, internal artifact id, or record id.
- `sourceType`: primary, secondary, social, HN discussion, internal, generated artifact, API record.
- `access`: public, internal, private, unknown.
- `date`: publish/update/event date when available.
- `retrievedAt`: date/time checked.
- `directFacts`: facts directly supported by the source.
- `interpretation`: agent synthesis or inference.
- `limits`: gaps, uncertainty, possible staleness, access caveats.
- `usableForPublic`: yes, no, or needs-review.

## Rules

- Keep quotes short and only when necessary.
- Do not treat snippets as source facts.
- Do not expose internal or private source details in public ledgers.
- If a source is internal, summarize the safe evidence boundary rather than pasting sensitive content.
- Preserve links to original sources and discussion/context pages separately.

## Minimal Markdown Shape

```markdown
## Source Ledger

| id | source | type | access | date | public-safe? | notes |
| --- | --- | --- | --- | --- | --- | --- |

## Direct Facts

- [S1] Fact.

## Interpretations

- Inference based on [S1] and [S2].

## Gaps

- Missing or unresolved item.
```
