# CookieJar Evidence

Use for read-only CookieJar activity lookups that feed participation/share distro workflows.

## Known Jar

HallMonitor CookieJar:

- chain: Gnosis `0x64`
- jar: `0x57cf76Af7771e6D22F0794A19B2533b71357d4F9`
- app: `https://www.cookiejar.wtf/jar/0x57cf76Af7771e6D22F0794A19B2533b71357d4F9`

## Read Model

Prefer contract reads over page scraping.

Useful contract/app state:

- `getWithdrawalDataArray`
- `accessType`
- `jarOwner`
- `currency`
- `currencyHeldByJar`
- `strictPurpose`

Expected withdrawal fields:

- amount
- purpose
- recipient

## Outputs

Produce:

- `cookiejar-withdrawals.json`
- `cookiejar-participation.md`

Include:

- month/cycle window
- jar address
- chain id
- token address/symbol if known
- recipient
- amount raw/display
- purpose
- timestamp/tx hash when available

## Rules

- Keep this read-only.
- Filter to the requested cycle/month window.
- If timestamps are missing, reconcile with transaction history or event logs before claiming period membership.
- Do not infer identity from address alone.
- Treat CookieJar as optional/historical evidence unless the reviewed cycle artifact says otherwise.
