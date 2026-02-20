# Concurrency Pattern Selection

Use this file when selecting a concurrency model.

## Decision guide
- Independent tasks with bounded parallelism -> worker pool.
- Multi-stage transformation -> pipeline.
- Multiple subcalls and merge -> fan-out/fan-in.
- Shared mutable state with strict ordering -> actor loop.
- Expensive downstream endpoint -> semaphore + rate limiter.

## Sizing hints
- CPU-bound workers: near `runtime.GOMAXPROCS(0)`.
- I/O-bound workers: start with downstream QPS and latency budget.
- Buffer sizes: keep small and observable; avoid "large by default".
