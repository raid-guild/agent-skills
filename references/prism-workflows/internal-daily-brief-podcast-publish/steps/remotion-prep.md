# Remotion Prep

## Outcome

Produce the canonical Remotion payload and a render plan artifact for the latest approved audio set.

## Use This Context

- `tts-manifest.json`
- segment MP3 artifacts
- any explicit scene / composition requirements from the latest human feedback

Use:
- `remotion-composition-checker` for live composition/schema validation
- `workflow-audio-bucket-uploader` for turning workflow audio into bucket-backed fetchable URLs

## Required Live Validation

Before writing the canonical payload:
- query `GET /compositions`
- if the chosen composition exposes a `schemaUrl`, fetch it
- build `remotion-input.json` to the live schema, not to an invented local shape

## Verified Bucket Pattern

Use the exact S3-compatible bucket contract from env:
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `STORAGE_S3_BUCKET`
- `STORAGE_S3_ENDPOINT`
- `STORAGE_S3_PREFIX`
- `STORAGE_S3_REGION`

The bucket itself is known-good. The critical requirement is that the final presigned GET URL must match the signed host/path exactly and must be anonymously fetchable before it is written into `props.segments[].url`.

## Remote Audio Rule

Use `workflow-audio-bucket-uploader`.

That means:
- upload every approved segment MP3 to the configured bucket/prefix
- generate deterministic object keys under `STORAGE_S3_PREFIX`
- generate absolute presigned GET `http(s)` URLs from the uploaded objects
- verify each presigned URL with an unauthenticated fetch before using it
- require that verification to return `200`
- only then write the URL into `props.segments[].url`
- do not fall back to service-token-only request artifact URLs

If a presigned URL returns `403`, treat that as a signing/path-style bug and fix the URL generation instead of continuing.

## DarkFactoryScene Contract

For `DarkFactoryScene`, use the live contract exactly:
- top-level `composition`
- optional `outputKey`
- `props.title`
- optional `props.accent`
- non-empty `props.segments[]`
- each segment with real remote `url` and positive `durationMs`
- optional `speaker` and `color`
- do not send `waveform`

## Durable Artifacts

Always write or refresh:
- `remotion-input.json`
- `render-plan.json`

The render plan should include at least:
- input artifact id
- output key
- composition id
- segment count
- total expected duration ms
- schema URL used when available
- bucket/prefix path used for uploaded audio
- uploaded object keys
- final verified presigned URLs or their deterministic source mapping
- whether shared-bucket audio URLs were created
- scene fingerprint or version marker when available
- whether this payload supersedes a prior render input
