# Event-Driven Fundamentals

## Event envelope
Required metadata:
- `event_id` (unique id)
- `event_type`
- `event_version`
- `occurred_at` (RFC3339)
- `producer`
- `trace_id` / `correlation_id`
- `key` (partition/grouping key)

## Contract rules
- Use schema registry or versioned schema files.
- Prefer backward-compatible additive changes.
- Never break existing consumers without deprecation window.

## Processing model
- Design consumers as idempotent.
- Separate transient failures from poison messages.
- Track lag, retries, and DLQ rates per consumer group.
