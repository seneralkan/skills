# Concurrency Test Plan

Use this file to validate correctness and reliability.

## Required

```bash
go test -race ./...
```

## Leak and shutdown checks

```bash
go test ./... -run TestGracefulShutdown -v
```

Add assertions for:
- cancellation propagation
- channel closure behavior
- partial failures in fan-in stages
- no blocked send/receive after shutdown

## Performance checks

```bash
go test -bench . -benchmem ./...
```

Compare changes with `benchstat` where possible.
