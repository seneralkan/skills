# Benchmarking Discipline

## Commands

```bash
go test -bench . -benchmem ./...
```

Repeat and compare:

```bash
go test -bench BenchmarkName -count=10 -benchmem ./...
```

## Rules
- Benchmark realistic input sizes.
- Isolate setup from measured section.
- Treat microbenchmarks as directional; validate with macro/load tests.
