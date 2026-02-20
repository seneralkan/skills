---
name: go-concurrency
description: Design, implement, and debug concurrency in Go services using goroutines, channels, worker pools, context cancellation, select patterns, and synchronization primitives. Use when users ask for throughput improvements, parallel processing, race/deadlock fixes, backpressure handling, fan-in/fan-out patterns, pipeline design, batch processing, safe shutdown, goroutine leak detection, or distributed coordination in Golang backends.
---

# Go Concurrency

## Quick start
1. Clarify workload type: CPU-bound, I/O-bound, or mixed.
2. Define correctness constraints: ordering, at-most-once, exactly-once, retries, idempotency.
3. Estimate load profile: steady-state throughput, burst size, downstream capacity.
4. Choose pattern: worker pool, pipeline, fan-out/fan-in, semaphore, batch processor, or actor-like loop.
5. Wire cancellation and timeout with `context.Context` from the entrypoint down.
6. Verify: race detector, goroutine leak checks, benchmarks, and production metrics.

## References
- Pattern selection heuristics: `references/pattern-selection.md`
- Concurrency-focused test plan: `references/concurrency-test-plan.md`

## Patterns reference

### Worker pool
- Fixed number of goroutines consuming from a shared input channel.
- Use when: processing a stream of independent tasks with bounded concurrency.
- Size workers by downstream capacity, not by input volume.

### Pipeline (staged fan-out/fan-in)
- Chain of stages connected by channels; each stage runs its own goroutine(s).
- Use when: data flows through sequential transformations with different parallelism needs per stage.
- Propagate errors via dedicated error channel or `errgroup`.

### Fan-out / fan-in
- Fan-out: dispatch work to multiple goroutines. Fan-in: merge results into one channel.
- Use when: independent subtasks can run in parallel and results must be aggregated.

### Batch processor
- Collect items into batches by size or time window, then flush.
- Use when: downstream prefers bulk operations (batch insert, bulk API call).
- Always flush remaining items on shutdown.

### Semaphore / rate limiter
- Use `x/sync/semaphore` or `golang.org/x/time/rate` to cap inflight or per-second operations.
- Use when: protecting a shared resource from overload (DB connections, external API quota).

### Actor-like loop
- Single goroutine owns mutable state; communicates via request/response channels.
- Use when: shared state management is complex and mutex nesting would be fragile.

## Design rules

### 1) Bound concurrency explicitly
- Never spawn unbounded goroutines for unbounded input.
- Cap workers by CPU cores, downstream capacity, and memory budget.
- Use buffered channels only when queue length is intentional, measured, and has backpressure handling.
- Apply `GOMAXPROCS`-aware sizing for CPU-bound work (consider `automaxprocs` in containers).

### 2) Manage lifecycle
- Tie every goroutine lifecycle to `context.Context` cancellation.
- Producers close output channels exactly once; use `sync.Once` if closure is conditional.
- Consumers terminate on `ctx.Done()` or channel close — always check both in `select`.
- Implement graceful shutdown with `signal.NotifyContext` at the service root.
- Use `errgroup.Group` to coordinate goroutine completion with first-error cancellation.
- Set a hard shutdown deadline after the graceful period expires.

### 3) Select patterns
- Always include a `case <-ctx.Done():` in every `select` to prevent goroutine leaks.
- Use `default` case only for non-blocking try-send/try-receive; never in hot loops without backoff.
- Combine `time.After` or `time.NewTimer` with `select` for timeout; prefer `context.WithTimeout` when possible.
- Use `time.NewTicker` over `time.Tick` to allow cleanup via `ticker.Stop()`.
- Handle channel nil assignment to dynamically disable select cases.

### 4) Pick the right primitive
- **Channels**: ownership transfer, pipeline stages, signaling between goroutines.
- **`sync.Mutex`**: in-memory shared state when simpler than channels; keep critical sections short.
- **`sync.RWMutex`**: only with measured read-heavy contention; profile before choosing.
- **`sync.WaitGroup`**: joining worker completion when errors are handled separately.
- **`x/sync/errgroup`**: when first error must cancel siblings and collect the error.
- **`x/sync/semaphore`**: resource-bound tasks (DB pool, file descriptors).
- **`sync.Once`**: lazy initialization of shared resources.
- **`sync.Map`**: only for append-mostly, key-stable maps with high read concurrency; prefer `Mutex` + `map` otherwise.
- **`atomic` package**: simple counters and flags; avoid for complex state.

### 5) Memory model awareness
- Go's memory model guarantees happen-before only through synchronization primitives.
- Never rely on goroutine scheduling order for correctness.
- Reads and writes to shared memory without synchronization are data races, even if "it works" locally.
- Use `go build -race` or `go test -race` to surface violations.

### 6) Prevent common failures
- **Goroutine leaks**: blocked sends/receives without `ctx.Done()` or channel close; detect with `goleak` in tests.
- **Deadlocks**: cyclic channel waits, missing channel closes, lock ordering violations.
- **Data races**: every shared mutable state must be guarded; no exceptions.
- **Silent failures**: never swallow `ctx.Err()`, timeout, or cancellation errors; log or propagate.
- **Premature optimization**: adding concurrency without profiling; measure first.
- **Channel misuse**: using channels as mutexes, or mutexes as channels; pick the right tool.

### 7) Distributed concurrency
- Use distributed locks (Redis, etcd) when coordination spans multiple instances.
- Implement leader election for singleton workloads in multi-replica deployments.
- Design partition-aware consumers for message queues (Kafka, SQS).
- Never rely on in-process synchronization for cross-instance coordination.

## Verify and tune
- Run `go test -race ./...` on every PR; zero tolerance for race reports.
- Add `goleak.VerifyTestMain` or per-test goroutine leak checks.
- Write table-driven tests for cancellation, timeout, partial failure, and graceful shutdown.
- Benchmark with `testing.B` before and after concurrency changes; compare with `benchstat`.
- Inspect `pprof` goroutine, block, and mutex profiles under load to confirm real gains.
- Monitor goroutine count, channel buffer utilization, and worker pool saturation in production.

## Output template
When implementing or reviewing concurrency, produce:
1. **Pattern**: selected concurrency pattern and rationale.
2. **Failure modes**: identified risks (leak, race, deadlock) and mitigations.
3. **Cancellation flow**: how shutdown propagates from signal to every goroutine.
4. **Backpressure**: how the system behaves when downstream is slower than upstream.
5. **Test plan**: `-race`, `goleak`, unit tests, benchmarks.
6. **Code diff**: minimal changes with comments only for non-obvious decisions.
