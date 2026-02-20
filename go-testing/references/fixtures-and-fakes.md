# Fixtures and Fakes

## Rules
- Use builders for test data, not raw JSON blobs everywhere.
- Keep fixtures small and explicit.
- Prefer in-memory fakes for unit tests.
- Use real dependencies in integration tests (containers/local services).

## Determinism
- Inject clock/time provider.
- Inject UUID/random generator where behavior depends on randomness.
- Avoid sleeps when waiting; poll with bounded timeout.
