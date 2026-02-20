# Kafka Producer/Consumer (Go)

## Producer
- Choose partition key based on ordering requirement.
- Enable idempotent producer where client/library supports it.
- Use acks strategy aligned to durability target (`all` for stronger guarantees).
- Batch with bounded linger and size settings.

## Consumer
- Use consumer groups for horizontal scaling.
- Commit offsets only after successful processing.
- Rebalance handlers must flush in-flight work safely.
- Pause/resume consumption for downstream backpressure.

## Failure handling
- Retry transient errors with bounded attempts.
- Route non-recoverable payloads to DLQ topic with reason metadata.
- Preserve original key/headers for replay tooling.
