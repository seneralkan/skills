---
name: go-best-practices
description: Apply and enforce Go backend engineering best practices across project structure, API design, error handling, configuration, observability, testing, security, performance, and delivery. Use when users ask for code review, refactor guidance, service hardening, maintainability improvements, production-readiness checks, dependency management, middleware design, or profiling in Golang services.
---

# Go Backend Best Practices

## Quick start
1. Identify service scope: API, worker, CLI, or mixed.
2. Audit baseline: layout, dependencies, config, logging, tests, CI/CD.
3. Map external dependencies: databases, caches, queues, third-party APIs.
4. Prioritize findings by risk: correctness → reliability → security → operability → performance.
5. Implement smallest safe diffs first; one concern per commit.
6. Verify with tests, race detector, linter, and staging rollout.

## Review checklist

### 1) Project structure
- Follow standard layout: `cmd/`, `internal/`, `pkg/` (only for truly public libs).
- Keep `main.go` minimal: wire dependencies and start the server.
- Avoid package cycles; use dependency injection over globals.
- Keep interfaces near consumers, not producers (Interface Segregation).
- Group by domain/feature, not by technical layer, when the service grows.
- Use `internal/` to prevent unintended external imports.

### 2) API and domain
- Validate request payloads strictly at boundaries; reject early.
- Keep handlers thin; push all business logic into service/usecase layer.
- Keep repository interfaces explicit, small, and mockable.
- Use DTOs at boundaries; do not leak domain structs to transport layer.
- Version APIs explicitly (URL path or header) from day one.
- Return consistent error response schemas across all endpoints.

### 3) Error handling
- Define domain error types (sentinel errors or typed errors) for known failure modes.
- Wrap errors with `fmt.Errorf("context: %w", err)` for traceability.
- Map domain errors to stable HTTP/gRPC status codes at the handler layer only.
- Never ignore errors except with explicit `//nolint` justification.
- Log errors once at the top of the call stack; avoid duplicate logging.
- Include operation context in error messages but never leak internal details to clients.

### 4) Context and timeouts
- Accept `context.Context` as first parameter on all external and I/O paths.
- Apply per-operation timeouts for DB, HTTP client, queue, and cache calls.
- Propagate cancellation to all downstream calls; never detach context silently.
- Use `context.WithTimeout` or `context.WithDeadline` over raw `time.After`.
- Check `ctx.Err()` before expensive operations inside loops.

### 5) Configuration and secrets
- Use typed config structs with startup-time validation (fail fast).
- Separate required and optional settings; document defaults.
- Never hardcode secrets; load from env vars, secret manager, or mounted volumes.
- Support config reloading for feature flags and non-critical settings.
- Validate configuration completeness before starting listeners.

### 6) Dependency management
- Pin direct dependencies; use `go mod tidy` and commit `go.sum`.
- Run `govulncheck` in CI to catch known vulnerabilities.
- Audit transitive dependencies periodically.
- Prefer stdlib and well-maintained libraries over niche packages.
- Wrap third-party SDKs behind internal interfaces for replaceability.

### 7) Middleware and cross-cutting concerns
- Apply middleware in consistent order: recovery → logging → auth → rate-limit → tracing → handler.
- Use middleware for request ID injection, CORS, and response compression.
- Keep middleware stateless; pass data via context values with typed keys.
- Avoid deeply nested middleware chains; prefer explicit composition.

### 8) Observability
- Use structured logging (slog or zerolog) with request correlation IDs.
- Expose `/health`, `/ready`, and `/metrics` endpoints.
- Add distributed tracing (OpenTelemetry or Newrelic based on the project) around external dependency calls.
- Emit latency, error rate, and saturation metrics per endpoint.
- Set log levels configurable at runtime; default to `info` in production.
- Include build version and instance metadata in startup logs.

### 9) Data and transactions
- Keep transaction scope minimal; prefer single-statement operations when possible.
- Make retries idempotent and bounded with exponential backoff.
- Guard against N+1 queries and unbounded result sets (always paginate).

### 10) Performance and profiling
- Profile before optimizing; use `pprof` (CPU, heap, goroutine, block).
- Reuse allocations: `sync.Pool` for hot-path buffers, pre-allocated slices.
- Avoid unnecessary reflection and interface boxing in critical paths.
- Use connection pooling for HTTP clients, DB, Redis, and gRPC.
- Set appropriate `GOMAXPROCS` for containerized environments (use `automaxprocs`).
- Benchmark critical paths with `testing.B` and track regressions in CI.

### 11) Testing and quality gates
- Write table-driven tests for business logic and edge cases.
- Use `testify` or stdlib subtests; keep test names descriptive.
- Add integration tests for DB, cache, and external adapters (use testcontainers or docker-compose).
- Generate and review test coverage; enforce minimum threshold in CI.
- Run `go vet ./...`, `staticcheck`, and `golangci-lint` in CI.
- Run `go test -race ./...` on every PR.
- Use golden files for complex output validation (serialization, templates).

### 12) Security
- Validate authn/authz at service boundaries; fail closed.
- Sanitize and validate all external input (query params, headers, body).
- Set CORS policies explicitly; never use wildcard in production.
- Apply rate limiting and request size limits at ingress.
- Use parameterized queries; never concatenate SQL.
- Rotate secrets and tokens; set short-lived credentials where possible.
- Enforce TLS for all external communication.

### 13) Delivery and operations
- Implement graceful shutdown: stop accepting, drain in-flight, close resources in order.
- Use readiness probes to prevent traffic before the service is fully initialized.
- Design for zero-downtime deployments (rolling update, blue-green).
- Pin container base images by digest; rebuild on security patches.
- Keep Dockerfiles minimal: multi-stage builds, non-root user, scratch or distroless.
- Document runbooks for common failure scenarios.

## Output template
When asked to review or improve a service, provide:
1. **Findings** ordered by severity (🔴 Critical → 🟡 Warning → 🔵 Info) with file and line references.
2. **Patch plan**: minimal, ordered diffs grouped by concern.
3. **Verification**: commands to run and expected outcomes.
4. **Trade-offs**: any cost, complexity, or migration risk introduced.
5. **Follow-up**: residual risks and recommended next steps.
