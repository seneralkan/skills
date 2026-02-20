# Error and Versioning Policy

## Error contract
- Provide stable `code`, human `message`, and optional `details`.
- Do not leak internals in external messages.
- Log full context server-side once.

## Versioning
- Prefer additive changes in same major version.
- Introduce new major version for breaking changes.
- Support deprecation windows with clear timeline.

## Idempotency
- Require idempotency keys for retriable write endpoints.
- Persist key + response hash for replay safety.
