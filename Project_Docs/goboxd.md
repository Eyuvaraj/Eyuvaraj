# goboxd

**Repository:** [goboxd](https://github.com/Eyuvaraj/goboxd) *(fork)*

## One-line summary
I built this Go HTTP service to compile and run untrusted source code against test cases inside per-request `nsjail` sandboxes. Built solo for Paradox IIT Madras 2026, it competed across three stages against 50+ teams, placed fifth in the final stage, and is open source on GitHub.

## Technology Stack
- Go 1.26, stdlib `net/http` + `chi` v5.2.2 router (chosen over gin/echo for plain `http.Handler` compat, per README)
- `nsjail` 3.4 (Google's syscall/namespace sandboxer) — vendored as a git submodule (`external/nsjail`), compiled from source in the Docker build
- Linux cgroup v2, seccomp-bpf (via Kafel policy string), Linux namespaces (PID/net/mount)
- `gopkg.in/yaml.v3` for declarative language config; `swaggo` for OpenAPI docs; Docker + Compose v2 for packaging
- Load/stress testing: `hey` and `vegeta` (Go HTTP load tools), Python (`matplotlib`) for plotting results

## Architecture
`cmd/goboxd/main.go` wires a `chi` router (`POST /run`, `POST /v1/run`, `GET /healthz|readyz|info`, plus a Swagger UI and browser playground) to `internal/handler` → `internal/runner`. `Runner.Submit` (`internal/runner/runner.go`) takes a concurrency-semaphore slot, creates a per-job temporary workspace (`internal/sandbox/workspace.go`), then `Job.compile()` and `runTests()` (`internal/runner/job.go`) call `sandbox.Run()` once per compile step and once per test case, each through a fresh `nsjail` subprocess. Results including stdout, stderr, exit code, memory peak, and CPU time are read back through pipes and a cgroup accounting file, mapped to statuses including `accepted`, `wrong_output`, `time_exceeded`, `memory_exceeded`, and `runtime_error`, and returned as JSON; structurally valid requests always return HTTP 200 with the execution outcome in the body.

## Isolation/sandboxing mechanism
Isolation is **not** Docker-per-request. Docker packages the service itself (the container runs unprivileged with only the added `SYS_ADMIN` and `SYS_PTRACE` capabilities and relaxed seccomp/system-path settings); the real sandbox boundary is **nsjail**, invoked as a subprocess per compile or run step through `internal/sandbox/nsjail.go` and `buildArgv`. Each invocation gets its own PID namespace using nsjail's default `CLONE_NEWPID`, a `chroot` to a throwaway per-job directory through `--chroot` and `--mode o`, a network namespace with no loopback or interfaces through `--iface_no_lo` verified by a live connection probe expecting `ENETUNREACH`, a dedicated cgroup v2 subtree for memory and PID accounting through `--cgroupv2_mount`, and an inline Kafel seccomp deny-list that terminates processes attempting `ptrace`, `mount`, `unshare`, `setns`, `chroot`, `bpf`, kernel-module syscalls, and related operations while otherwise using `DEFAULT ALLOW`. A dedicated adversarial test harness under `tests/sandbox/` uses 15 probes, including Python and C fork bombs, chroot and ptrace escape attempts, `/etc/passwd` reads, network connections, and output, memory, and disk bombs, to verify containment against a live instance and flag any breach.

## Resource limiting & concurrency model
- **Wall time:** `--time_limit` (nsjail) plus `--rlimit_cpu` set 1s higher as a backstop so nsjail's own timer fires first
- **Memory:** `--cgroup_mem_max` + `--cgroup_mem_swap_max 0`; OOM is detected by reading the per-job cgroup's `memory.events` (`oom_kill` field) because nsjail only surfaces a cgroup OOM as a bare SIGKILL
- **Processes/threads:** `--cgroup_pids_max` + `--rlimit_nproc`
- **Disk:** `--rlimit_fsize 100` (100 MB per file)
- **Output:** stdout/stderr capped via `io.LimitReader` in Go (`readCapped`), draining the rest so the child process never blocks
- **Concurrency:** a buffered `chan struct{}` semaphore sized to `MAX_CONCURRENT_JOBS` (default = host CPU count); an atomic queue-depth counter sheds excess requests with `503` + `Retry-After` once `MAX_QUEUE_DEPTH` is exceeded (0 = unbounded queue, requests wait rather than fail)

## Supported languages / API surface
15 languages via declarative YAML (`configs/languages.yaml`) — adding one needs only a YAML entry + install script, no Go changes. `POST /run` is the base contract; `POST /v1/run` adds raw single-run execution (no test cases), per-test exit codes, and a custom "evaluator" mode where a user-supplied grading program scores each test's output (returns a JSON verdict) instead of exact-match comparison.

## Scale and Quality
The project contains roughly 6,000 lines of Go and 16 test files. GitHub Actions runs unit tests, `govulncheck`, linting, Docker builds, and Docker-based integration tests. Load testing with `hey` and `vegeta` sustained 503 requests per second at 50 concurrent clients with zero errors on an Apple M4. A constrained JVM workload exposed a throughput ceiling of approximately 5 requests per second under a 2 vCPU and 2 GB memory limit, which informed concurrency tuning.

## Notable engineering decisions
- Correctly separating the container's own Docker capabilities (needed only so nsjail can create nested namespaces) from nsjail's independent namespace/cgroup/seccomp sandbox, which is the actual security boundary for untrusted code
- Layered defense: capability dropping, chroot, network namespace, and seccomp each independently block the same escape class (e.g., `chroot()` blocked by both missing `CAP_SYS_CHROOT` and the seccomp deny-list)
- Reading cgroup `memory.events` to distinguish an OOM kill from an ordinary crash, since nsjail's process exit code alone can't disambiguate
- A queue-never-fails design (bounded semaphore + optional bounded queue with 503 shedding) instead of dropping or erroring under burst load

## Highlights
- Architected a Go service that sandboxes untrusted code across 15 languages using `nsjail` (Linux namespaces, cgroup v2, seccomp-bpf), enforcing per-job CPU/memory/process limits.
- Designed a 15-probe adversarial test harness covering fork bombs, ptrace and chroot escapes, network breakouts, and filesystem access.
- Load-tested the execution API with `hey` and `vegeta`, sustaining 503 req/s at 50 concurrent clients with zero errors.
- Diagnosed a JVM-workload throughput ceiling of ~5 req/s under a 2 vCPU/2GB constraint, tracing the bottleneck to the concurrency semaphore size.
- Implemented cgroup-based OOM detection via `memory.events`, distinguishing memory-limit kills from ordinary crashes that nsjail otherwise reports identically as SIGKILL.
