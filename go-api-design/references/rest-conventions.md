# REST Conventions

## Resource and path design
- Use nouns, not verbs, for resource paths.
- Prefer `/v1/resources/{id}` style versioning.
- Keep nesting shallow.

## Requests
- Validate query/body/path strictly.
- Enforce request size limits.
- Use explicit filter and sort parameters.

## Responses
- Return stable envelope for list APIs:
  - `items`
  - `next_cursor`
  - `has_more`
- Keep timestamps in RFC3339.
