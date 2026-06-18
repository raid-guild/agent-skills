# DuckDuckGo / ddgs Fallback

Use this only as a fallback or when DuckDuckGo results are specifically requested.

Codex/browser web search is preferred when available. Do not add a DuckDuckGo dependency just to duplicate an existing search tool.

## Boundary

DuckDuckGo's official Instant Answer API is useful for some entity/topic summaries, but it is not a full ranked web search results API.

For keyless web search, the practical path is usually `ddgs`, a third-party DuckDuckGo search package/CLI. Treat it as an unofficial HTML-backed/provider-dependent search path that can break or be rate-limited.

## Runtime Checks

Before using `ddgs`, check availability:

```bash
command -v ddgs
```

If the CLI exists, prefer CLI usage over assuming a Python runtime can import the package.

Only use Python after verifying the same runtime can import `ddgs`.

## CLI Examples

```bash
ddgs text -q "query terms" -m 5 -o json
ddgs news -q "query terms" -m 5 -o json
ddgs images -q "query terms" -m 5 -o json
ddgs videos -q "query terms" -m 5 -o json
```

Common flags:

- `-q`: query
- `-m`: max results
- `-r`: region, such as `us-en`
- `-t`: time window, such as `d`, `w`, `m`, `y`
- `-s`: safe search
- `-o json`: JSON output

## Rules

- Search results are leads, not evidence.
- Extract/read the selected source before relying on details.
- Use `.get()` or equivalent defensive parsing because result fields vary.
- If results are empty, retry with clearer keywords or use another search path.
- Do not install dependencies unless the operator wants this fallback prepared in the runtime.
