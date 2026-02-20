# Memory Optimization

## Tactics
- Reduce allocations in hot loops.
- Reuse buffers where safe.
- Pre-size slices and maps when cardinality is known.
- Avoid reflection-heavy generic paths in critical code.

## GC considerations
- Avoid premature `sync.Pool` usage without measurement.
- Track GC pause and heap growth with runtime metrics.
- Optimize object lifetime and escape patterns first.
