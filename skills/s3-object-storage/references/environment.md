# Environment

Use environment/config as the source of truth for S3-compatible storage.

Common variables:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_SESSION_TOKEN`, if used
- `STORAGE_S3_BUCKET`
- `STORAGE_S3_ENDPOINT`
- `STORAGE_S3_PREFIX`
- `STORAGE_S3_REGION`

Do not print raw credential values.

## Compatibility

The storage backend may be AWS S3, Cloudflare R2, MinIO, DigitalOcean Spaces, or another S3-compatible service.

Check:

- endpoint URL style
- bucket/path addressing expectations
- region requirement
- ACL/public-read policy
- content type behavior
- final URL shape

## Missing Config

If required config is missing, fail before upload and list missing variable names only.
