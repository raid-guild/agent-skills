---
name: s3-object-storage
description: Use when Codex needs to upload, inspect, plan, or document S3-compatible object storage operations, including storing local files or workflow artifacts, creating deterministic object keys, setting content types, producing fetchable URLs, recording bucket/key/url evidence, avoiding credential leakage, and preparing media or document assets for downstream services. Not specific to Remotion; media/render skills should route here for generic storage work.
---

# S3 Object Storage

Use this skill for generic S3-compatible object storage operations.

This skill owns upload/key/url/evidence behavior. It does not own Remotion payloads, content strategy, public publishing, or media render diagnostics.

## Routing

Read only the references needed:

- Environment and credentials: `references/environment.md`
- Key and URL policy: `references/key-and-url-policy.md`
- Upload evidence and failure handling: `references/evidence-and-failures.md`

Use `rg-media-render-ops` for Remotion/render payload logic.

## Operating Rules

- Treat credentials as secrets.
- Do not print access keys, secret keys, session tokens, signed URLs with private credentials, or raw env values.
- Use deterministic keys when retries or reconciliation matter.
- Preserve existing uploaded object/key when it already matches the intended artifact.
- Return absolute fetchable URLs only when the configured bucket/endpoint makes them fetchable by the downstream consumer.
- Record bucket, endpoint, region, prefix, object key, content type, source artifact, and final URL when available.

## Workflow

1. Identify source file/artifact and intended consumer.
2. Determine bucket, endpoint, region, and prefix from environment/config.
3. Build a deterministic object key.
4. Set appropriate content type.
5. Upload or prepare upload command.
6. Verify or construct fetchable URL.
7. Return durable evidence and safe failure details.

## Output

```text
Object storage plan/result:
- source:
- bucket:
- endpoint:
- region:
- prefix:
- object key:
- content type:
- fetchable URL:
- evidence:
- blockers:
```
