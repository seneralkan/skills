---
name: go-microservices
description: Design and operate Go microservices with synchronous and asynchronous communication, event-driven workflows, resilience patterns, and safe producer-consumer architectures across Kafka, Amazon SQS/SNS, and RabbitMQ. Use when users ask for microservice decomposition, event contracts, queue/topic design, retries, dead-letter handling, idempotency, saga orchestration, or Go service-to-service reliability.
---

# Go Microservices

## Quick start
1. Define service boundaries and ownership.
2. Choose interaction mode per use case: sync API vs async event.
3. Establish event contracts, schema evolution, and compatibility policy.
4. Implement producer-consumer reliability: retries, DLQ, idempotency, observability.

## Workflow
1. Model commands/events and ownership per bounded context.
2. Standardize envelope metadata (event id, key, timestamp, version, trace id).
3. Implement producer guarantees and consumer processing semantics.
4. Add replay safety, poison-message handling, and backpressure controls.
5. Validate with contract tests and failure-injection scenarios.

## References
- Event architecture fundamentals: `references/event-driven-fundamentals.md`
- Kafka producer/consumer patterns: `references/kafka-producer-consumer.md`
- SQS/SNS producer/consumer patterns: `references/sqs-sns-producer-consumer.md`
- RabbitMQ producer/consumer patterns: `references/rabbitmq-producer-consumer.md`
- Reliability patterns (retry, DLQ, idempotency, outbox): `references/reliability-patterns.md`

## Output template
1. Topology proposal (services, topics/queues, ownership).
2. Producer and consumer contract definitions.
3. Delivery semantics and failure-mode mitigation plan.
4. Operational checklist (metrics, alerts, runbooks).
