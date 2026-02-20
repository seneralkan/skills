# CI Quality Gates

Run these in CI for Go services:

```bash
go test ./...
go test -race ./...
go test -coverprofile=coverage.out ./...
go tool cover -func=coverage.out
staticcheck ./...
golangci-lint run
```

## Policy
- Block merge on race detector failures.
- Block merge when changed packages reduce coverage below agreed threshold.
- Quarantine flaky tests and track owner + fix deadline.
