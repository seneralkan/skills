---
name: go-api-design
description: Design and review Go service APIs (REST and gRPC) for correctness, consistency, versioning, pagination, error contracts, idempotency, and backward compatibility. Use when users ask for endpoint design, API refactoring, schema evolution, request/response modeling, or production-grade API governance in Go backends.
---

# Go API Design

## Quick start
1. Define consumer personas and compatibility requirements.
2. Lock error contract and versioning strategy early.
3. Model requests/responses with strict validation.
4. Add pagination, filtering, idempotency, and observability defaults.

## Workflow
1. Specify resource model and naming conventions.
2. Define request/response DTOs and validation rules.
3. Standardize error schema and status mapping.
4. Validate backward compatibility and rollout plan.

## References
- REST conventions: `references/rest-conventions.md`
- gRPC conventions: `references/grpc-conventions.md`
- Error and compatibility policy: `references/error-and-versioning.md`

## Output template
1. API findings by severity.
2. Revised endpoint/schema proposal.
3. Compatibility impact and migration steps.
4. Test and rollout checklist.
