---
name: go-testing
description: Design and enforce robust testing in Go services using unit, integration, contract, and end-to-end strategies with table-driven tests, mocks, fixtures, race checks, and CI quality gates. Use when users ask for test planning, flaky test fixes, coverage improvements, regression prevention, test refactors, or reliable Go test automation.
---

# Go Testing

## Quick start
1. Map test pyramid scope: unit, integration, contract, e2e.
2. Identify high-risk paths first: money flow, auth, idempotency, retries.
3. Stabilize foundations: deterministic clocks, isolated fixtures, clean teardown.
4. Add race, lint, and coverage gates to CI.

## Workflow
1. Start with deterministic unit tests for core domain logic.
2. Add integration tests for adapters (DB/cache/queue/http).
3. Add contract tests for external APIs and schema assumptions.
4. Add targeted e2e for critical user journeys only.
5. Keep fast feedback by separating smoke vs full suites.

## References
- Test design matrix: `references/test-matrix.md`
- Isolation and fixtures: `references/fixtures-and-fakes.md`
- CI gates and commands: `references/ci-quality-gates.md`

## Output template
1. Test gaps by risk (critical, high, medium).
2. Minimal test plan with file-level targets.
3. Proposed test cases (inputs, expected outputs, edge cases).
4. Verification commands and pass criteria.
