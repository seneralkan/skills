# Test Matrix

Use this matrix to decide test type per change.

## Unit tests
- Pure business rules and validation logic.
- Error mapping and edge-case branching.

## Integration tests
- SQL queries, transactions, migrations.
- Redis/cache behavior and TTL semantics.
- Queue publish/consume behavior.

## Contract tests
- Third-party API request/response schemas.
- Compatibility with protobuf/openapi changes.

## End-to-end tests
- Minimal critical flows only.
- Keep counts low, assertions high-value.
