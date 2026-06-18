---
name: workflow-audio-bucket-uploader
description: Use this skill when Codex needs to upload workflow-generated audio files to the configured S3-compatible storage bucket, produce fetchable URLs for Remotion or other media services, and avoid using service-token-only artifact URLs as render inputs.
---

# Workflow Audio Bucket Uploader

Use this skill when a workflow has audio artifacts that must be made fetchable by an external renderer such as Remotion.

## Required Environment

Use these exact environment variables:
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `STORAGE_S3_BUCKET`
- `STORAGE_S3_ENDPOINT`
- `STORAGE_S3_PREFIX`
- `STORAGE_S3_REGION`

Treat these variables as the source of truth for the workflow audio bucket contract.

## Use This Skill For

- uploading TTS MP3 segments for Remotion render input
- turning private workflow artifact audio into bucket-backed fetchable URLs
- generating deterministic object keys for workflow media inputs
- recording which uploaded URLs were used in `remotion-input.json` and `render-plan.json`

## Operating Rules

- Do not point Remotion at request-artifact URLs that require `x-service-token`.
- Upload the approved audio files to the configured bucket first.
- Use stable deterministic object keys under `STORAGE_S3_PREFIX` so retries can reconcile prior uploads.
- Prefer preserving an existing uploaded object/key for the same artifact content instead of creating needless duplicates.
- Return absolute `http(s)` URLs that the renderer can fetch.

## Key Construction

Use a deterministic per-request path under `STORAGE_S3_PREFIX`, for example:
- workflow key
- request number or request id
- input artifact id or TTS segment order
- filename

The goal is that reruns for the same approved audio can find or overwrite the intended object predictably.

## Remotion Contract

When building a Remotion payload:
- each `props.segments[].url` must be a fetchable absolute URL
- each segment must still include positive `durationMs`
- later steps should not need service-token auth to fetch the audio

## Durable Evidence

When this skill is used, workflows should record:
- bucket name
- endpoint
- region
- prefix path used
- final object key per uploaded segment when available
- final absolute URL per segment

## Failure Handling

If upload or URL generation fails:
- fail before render submission
- explain whether the failure was credential, bucket, endpoint, prefix, or URL-generation related
- do not fall back to service-token-only artifact URLs
