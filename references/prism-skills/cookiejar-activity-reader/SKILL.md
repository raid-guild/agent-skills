---
name: cookiejar-activity-reader
description: Use this skill when Codex needs to read a CookieJar V3 jar onchain, extract monthly withdrawals and purposes, and turn them into share-distro evidence artifacts for Prism workflows.
---

# CookieJar Activity Reader

Use this skill for read-only CookieJar activity lookups that feed monthly share-distro workflows.

## Purpose

This skill exists to turn a known CookieJar V3 jar into structured monthly participation evidence.

For RaidGuild share distro, a CookieJar withdrawal in the target month counts as CookieJar participation. When available, include the onchain withdrawal purpose as supporting evidence.

## Current known jar

- HallMonitor CookieJar:
  - chain: Gnosis `0x64`
  - jar: `0x57cf76Af7771e6D22F0794A19B2533b71357d4F9`
  - app link: `https://www.cookiejar.wtf/jar/0x57cf76Af7771e6D22F0794A19B2533b71357d4F9`

## What to read

Prefer contract reads over page scraping.

The CookieJar V3 app for this jar reads contract state including:
- `getWithdrawalDataArray`
- `accessType`
- `jarOwner`
- `currency`
- `currencyHeldByJar`
- `strictPurpose`

For historical activity, the key source is `getWithdrawalDataArray`. For this jar, the app renders each withdrawal with:
- `amount`
- `purpose`
- `recipient`

Treat `purpose` as onchain withdrawal history data when returned by the contract.

## Expected output

When used in a workflow, produce one or both of these artifacts:

1. `cookiejar-withdrawals.json`
- month window used
- jar address
- chain id
- token address
- token symbol if known
- normalized withdrawals array with:
  - recipient
  - amountRaw
  - amountDisplay
  - purpose
  - timestamp if available
  - txHash if available

2. `cookiejar-participation.md`
- concise summary of who withdrew in the month
- grouped by recipient address
- include purpose lines when available
- clearly state that a withdrawal in the month counts as CookieJar participation for HallMonitor distro

## Workflow guidance

- Filter to the workflow target month in UTC.
- If the contract output lacks timestamps, reconcile with transaction history or event logs before claiming month membership.
- Do not infer a recipient identity from an address alone. Use HallMonitor or other approved mapping sources to resolve addresses to Discord handles.
- If no withdrawals exist in the month, say so directly and still write an artifact stating the checked month and jar.
- Keep this skill read-only. Do not withdraw, configure, or administer jars.
