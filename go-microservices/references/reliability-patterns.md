# Reliability Patterns

## Idempotency
- Store processed message ids with TTL/window.
- Guard side effects with idempotency key checks.

## Retry policy
- Exponential backoff with jitter.
- Cap attempts and escalate to DLQ.
- Classify errors: retryable vs non-retryable.

## Outbox pattern
- Write state change and outbox event in same DB transaction.
- Background dispatcher publishes outbox rows reliably.
- Mark sent events atomically and support replay tooling.

## Observability
Track per producer/consumer:
- publish latency and failures
- consumer lag / queue depth
- retry count and DLQ rate
- handler success/failure duration
