# Privacy And Verification

Treat CRM data as private by default.

## Privacy Rules

- Do not expose API tokens.
- Do not publish client, prospect, contact, deal, contract, or document details without approval.
- Summarize sensitive document content instead of copying raw text.
- Do not store private CRM exports in public repos.
- Use public output safety before publishing CRM-derived content.

## Verify Before

Verify exact intent before:

- creating or updating client/prospect records from uncertain source material
- soft deletes
- campaign sends
- bulk enrichment
- linking/unlinking documents across entities
- exporting reports
- sharing CRM-derived summaries outside the intended audience

## Operator Framing

The agent assists the operator. Verification catches wrong record, wrong audience, wrong campaign, or privacy mistakes; it does not second-guess operator judgment.
