# Ports and Adapters

## Port types
- Inbound ports: application capabilities exposed to handlers/jobs.
- Outbound ports: interfaces for persistence, messaging, external APIs.

## Adapter rules
- Each adapter implements one or more outbound ports.
- Adapter-specific errors are translated to domain/application errors.
- Retries/timeouts/circuit-breaking live in adapter layer.

## Example mapping
- HTTP handler -> inbound port (`CreateOrder` use case).
- Use case -> outbound ports (`OrderRepo`, `PaymentGateway`, `EventPublisher`).
