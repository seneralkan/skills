# Project Layout

Use this file when evaluating package boundaries and dependency flow.

## Recommended baseline
- `cmd/<service>/main.go`: wire dependencies only.
- `internal/<domain>`: core business logic, private to module.
- `internal/adapters/<transport|storage>`: HTTP/gRPC/DB integrations.
- `internal/platform`: cross-cutting concerns (config, logging, tracing).
- `pkg/`: only reusable APIs meant for other modules.

## Package rules
- Keep interfaces near consumers.
- Prevent import cycles by extracting shared contracts, not shared implementations.
- Avoid utility packages that become a dumping ground.
- Keep DTOs at transport boundaries; keep domain entities inside domain packages.

## Dependency direction
- Handlers -> services -> repositories/adapters.
- Domain code must not import transport-specific packages.
- External SDKs should be wrapped by internal interfaces.
