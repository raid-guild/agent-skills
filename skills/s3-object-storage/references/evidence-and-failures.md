# Evidence And Failures

## Evidence

Record:

- source path or artifact id
- bucket
- endpoint
- region
- prefix
- object key
- content type
- object size when available
- final URL
- upload time

Do not record credential values.

## Failure Classes

Classify failures as:

- missing config
- credential/auth
- bucket not found
- endpoint/region mismatch
- permission/ACL
- content type
- URL construction
- network timeout
- downstream fetch failure

Do not fall back to private service-token artifact URLs when the downstream consumer requires a public/fetchable URL.
