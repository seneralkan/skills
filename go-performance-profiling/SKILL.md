---
name: go-performance-profiling
description: Profile and optimize Go applications with pprof, benchmark-driven tuning, memory and allocation analysis, contention tracing, and production-safe performance improvements. Use when users ask for latency/throughput optimization, CPU or memory regressions, goroutine contention analysis, or Go performance hardening.
---

# Go Performance Profiling

## Quick start
1. Define SLO target and baseline metrics.
2. Reproduce workload representative of production.
3. Capture profiles (CPU, heap, goroutine, mutex, block).
4. Optimize hot paths only after evidence.
5. Re-measure and compare before/after.

## Workflow
1. Establish baseline benchmark and p95/p99 latency.
2. Identify top hotspots from profile evidence.
3. Apply smallest safe optimization.
4. Verify correctness and regression risk.
5. Document trade-offs and rollback path.

## References
- Profiling commands: `references/pprof-playbook.md`
- Allocation and GC tuning: `references/memory-optimization.md`
- Benchmark discipline: `references/benchmarking.md`

## Output template
1. Baseline and target metrics.
2. Hotspot summary with evidence.
3. Minimal optimization patch plan.
4. Benchmark/profile comparison.
5. Risks and guardrails.
