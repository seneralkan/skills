# Layers and Dependency Rule

## Layers
- Domain: entities, value objects, business rules.
- Application: use cases, orchestration, transaction boundaries.
- Interface adapters: HTTP/gRPC handlers, repositories, presenters.
- Infrastructure: DB drivers, messaging clients, framework bootstrapping.

## Dependency rule
- Source code dependencies point inward only.
- Domain must not import transport or persistence frameworks.
- Infrastructure depends on application/domain, never the reverse.

## Practical checks
- Keep framework types at boundaries.
- Convert DTO <-> domain in adapters.
- Keep domain pure and deterministic for fast unit tests.
