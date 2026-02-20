---
name: go-clean-architecture
description: Design, review, and refactor Go services using clean architecture and hexagonal patterns with strict dependency direction, use-case isolation, ports/adapters boundaries, and testable domain logic. Use when users ask for architecture redesign, layering cleanup, dependency inversion, monolith modularization, or maintainable Go backend structure.
---

# Go Clean Architecture

## Quick start
1. Map current layers and dependency directions.
2. Isolate core domain and use-case logic from frameworks.
3. Define ports for external I/O and adapters for implementations.
4. Enforce dependency rule in code and tests.

## Workflow
1. Identify domain entities and business invariants.
2. Move orchestration into use-case/application services.
3. Define inbound and outbound ports.
4. Implement adapters (HTTP, DB, queue, cache) behind ports.
5. Add architecture tests and package-boundary checks.

## References
- Layers and dependency rules: `references/layers-and-dependency-rule.md`
- Ports and adapters patterns: `references/ports-and-adapters.md`
- Refactor playbook for legacy services: `references/refactor-playbook.md`

## Output template
1. Architecture findings by severity.
2. Target package structure and dependency graph.
3. Incremental refactor plan with minimal risk.
4. Test strategy for boundary safety.
