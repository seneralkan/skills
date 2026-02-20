# RabbitMQ Producer/Consumer (Go)

## Producer
- Choose exchange type correctly (`direct`, `topic`, `fanout`).
- Publish persistent messages for durable flows.
- Use publisher confirms for delivery acknowledgement.

## Consumer
- Use manual ack mode for at-least-once guarantees.
- Set `prefetch` to control in-flight load.
- Use separate queues for slow vs fast consumers when needed.

## Failure handling
- Use dead-letter exchanges for rejected/expired messages.
- Nack with requeue only for transient errors.
- Avoid infinite requeue loops; cap retries via headers/counters.
