# pprof Playbook

## Capture

```bash
go test -run ^$ -bench . -cpuprofile cpu.out -memprofile mem.out ./...
go tool pprof -http=:8080 cpu.out
go tool pprof -http=:8081 mem.out
```

## Runtime endpoints
- Expose `/debug/pprof/` only in secured environments.
- Capture goroutine, mutex, and block profiles during load.

## Read hotspots
- Focus on cumulative time and allocation-heavy paths.
- Verify hotspot repeats across multiple captures.
