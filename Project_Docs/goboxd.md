# goboxd

## One-line summary
Go HTTP service that compiles and runs untrusted source code against test cases inside per-request `nsjail` sandboxes. Built solo for Paradox IIT Madras 2026, goboxd competed across three stages against 50+ teams, placed fifth in the final stage, and is open source on GitHub.

## Technology Stack
- Go 1.26, stdlib `net/http` + `chi` v5.2.2 router (chosen over gin/echo for plain `http.Handler` compat, per README)
- `nsjail` 3.4 (Google's syscall/namespace sandboxer) — vendored as a git submodule (`external/nsjail`), compiled from source in the Docker build
- Linux cgroup v2, seccomp-bpf (via Kafel policy string), Linux namespaces (PID/net/mount)
- `gopkg.in/yaml.v3` for declarative language config; `swaggo` for OpenAPI docs; Docker + Compose v2 for packaging
- Load/stress testing: `hey` and `vegeta` (Go HTTP load tools), Python (`matplotlib`) for plotting results

## Architecture
`cmd/goboxd/main.go` wires a `chi` router (`POST /run`, `POST /v1/run`, `GET /healthz|readyz|info`, plus a Swagger UI and browser playground) to `internal/handler` → `internal/runner`. `Runner.Submit` (internal/runner/runner.go) takes a concurrency-semaphore slot, creates a per-job temp workspace (`internal/sandbox/workspace.go`), then `Job.compile()`/`runTests()` (internal/runner/job.go) shell out to `sandbox.Run()` once per compile step and once per test case, each a fresh `nsjail` subprocess. Results (stdout/stderr, exit code, memory peak, CPU ms) are read back via pipes and a cgroup accounting file, then mapped to a status (`accepted`, `wrong_output`, `time_exceeded`, `memory_exceeded`, `runtime_error`, etc.) and returned as JSON — structurally valid requests always return HTTP 200, with the outcome in the body.

## Isolation/sandboxing mechanism
Isolation is **not** Docker-per-request. Docker packages the goboxd service itself (README: "container runs unprivileged with two added capabilities `SYS_ADMIN`/`SYS_PTRACE`... seccomp/systempaths unconfined"); the real sandbox boundary is **nsjail**, invoked as a subprocess per compile/run step (`internal/sandbox/nsjail.go`, `buildArgv`). Each invocation gets its own PID namespace (nsjail's default `CLONE_NEWPID`), a `chroot` to a throwaway per-job directory (`--chroot`, `--mode o`), a network namespace with no loopback/interfaces (`--iface_no_lo`, verified via a live "connect to 8.8.8.8" probe expecting `ENETUNREACH`), a dedicated cgroup v2 sub-tree for memory/PID accounting (`--cgroupv2_mount`), and a Kafel seccomp deny-list (`--seccomp_string`, defined inline in `nsjail.go`) that `KILL_PROCESS`es on `ptrace`, `mount`, `unshare`, `setns`, `chroot`, `bpf`, kernel-module syscalls, etc., with `DEFAULT ALLOW` otherwise. A dedicated adversarial test harness (`tests/sandbox/`, 15 probes: fork bombs in Python and C, chroot/ptrace escape attempts, `/etc/passwd` reads, network connects, output/memory/disk bombs) posts each attack to a live instance and checks the returned status for containment vs. "BREACH."

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
