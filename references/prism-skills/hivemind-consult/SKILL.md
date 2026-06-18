---
name: hivemind-consult
description: Use this skill when Codex needs to consult the Hivemind marketing strategy copilot, search Hivemind knowledge, or use Hivemind project/conversation context through the Hivemind API. Requires HIVE_MIND_API_KEY or HIVEMIND_API_KEY for authenticated calls.
---

Use this skill to consult Hivemind's marketing strategy knowledge base and AI personas from Codex.

Hivemind API base: `https://hivemind.myosin.xyz`
Docs: `https://hivemind.myosin.xyz/api-docs`

## When To Use

Use this skill when the user asks to consult Hivemind, ask the hive, search Hivemind knowledge, or get positioning, GTM, launch, growth, content, or marketing strategy guidance from Hivemind.

Do not use this skill for unrelated general web research. Hivemind is a marketing strategy copilot, not a replacement for factual verification or current news browsing.

## Credentials

Authenticated endpoints require an API key in the `x-api-key` request header.

Check credentials in this order:

1. `HIVE_MIND_API_KEY`
2. `HIVEMIND_API_KEY`

Rules:

1. Never print, echo, log, persist, or include the API key in artifacts.
2. Before authenticated calls, check only whether a key exists, not its value.
3. If neither env var is present, say the Hivemind key is not available in this runtime and stop before authenticated requests.
4. Health checks are open and can be used without a key: `GET /api/v1/chat` and `GET /api/knowledge/search`.

## API Shapes

### Chat

`POST /api/v1/chat` sends a message and returns an AI response grounded in Hivemind's corpus and optional project context.

Request fields:

- `text` or `query`: required string, 1-8000 characters.
- `stream`: optional boolean. Default `false`. Prefer JSON responses in Codex unless streaming is explicitly useful.
- `persona`: optional. Valid values: `genius-strategist`, `gtm-architect`, `ghostwriter`, `general-assistant`.
- `projectId`: optional UUID. Adds project social/intelligence context when the key has access.
- `startConversation`: optional boolean. Requires `projectId`; not all keys support persistence.
- `conversationId`: optional UUID. Appends to an existing conversation owned by the key's user. Do not send with `startConversation`.

Use chat for synthesized strategy answers. Prefer `persona: "gtm-architect"` for launch/GTM questions, `ghostwriter` for copy/content, `genius-strategist` for high-level positioning and strategic diagnosis, and omit persona when classification should decide.

### Knowledge Search

`POST /api/knowledge/search` searches the curated knowledge corpus directly. Use it when the user asks for sources, prior art, examples, or retrieval rather than a synthesized answer.

Keep requests minimal: send the query text and only add filters/project/persona fields when the user provides a reason. `projectId` gates endpoint access for search, but search results are global and are not filtered by project.

### Projects And Conversations

Use these only to discover IDs or resume explicit context:

- `GET /api/v1/projects`: list projects the key can access. Capped at 100; newest first.
- `GET /api/v1/projects/:id`: inspect a project's current state and enrichment status.
- `GET /api/v1/conversations`: list persistent conversations owned by the key's attributed user and scoped to accessible projects.

Do not create or patch projects unless the user explicitly asks for project management through Hivemind.

## Calling Pattern

Use Node's built-in `fetch` from the shell. Keep output small and redact sensitive headers.

```bash
node <<'HIVE'
const key = process.env.HIVE_MIND_API_KEY || process.env.HIVEMIND_API_KEY;
if (!key) throw new Error('Hivemind API key is not set');
const body = { text: 'QUESTION_HERE', persona: 'gtm-architect', stream: false };
const res = await fetch('https://hivemind.myosin.xyz/api/v1/chat', {
  method: 'POST',
  headers: { 'content-type': 'application/json', 'x-api-key': key },
  body: JSON.stringify(body)
});
console.log(res.status, res.headers.get('content-type'));
console.log((await res.text()).slice(0, 12000));
HIVE
```

## Response Handling

When answering the user:

1. State that the answer is from Hivemind when you used it.
2. Preserve useful source titles/authors returned by Hivemind, but do not invent citations if the response has none.
3. Separate Hivemind's claims from your own follow-up analysis when you add engineering or operational judgment.
4. Mention rate-limit or quota errors plainly and include reset/retry timing if headers provide it.
5. For 403 `project_access_denied`, ask for a different project ID or key scope; do not infer whether the project exists.
