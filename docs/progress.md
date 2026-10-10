# Progress and verification

## Current status

- [x] Go and MySQL selected as the project stack.
- [x] MIT License retained.
- [x] Non-business HTTP bootstrap, process health, timeouts, and shutdown handling written.
- [x] English documentation and the preparation roadmap rewritten.
- [x] Go scaffold build and runtime checks recorded.
- [ ] Catalog schema and fictional data written and verified by the maintainer.
- [ ] Database connection and catalog APIs implemented.
- [ ] Customer/order relationships implemented.
- [ ] Transactions, concurrency, cancellation, and retries verified.
- [ ] Query measurements, packaging, and interview review completed.

## Environment evidence

- On 2026-10-10, `go version` reported `go1.26.0 windows/amd64`.
- On 2026-10-09, the maintainer's Workbench screenshot showed successful database creation/selection and `SELECT VERSION()` returning MySQL `8.0.45`.
- That earlier database observation is environment evidence, not proof that the clean Go project has a schema or can connect to MySQL.

## Scaffold verification

### Go scaffold: 2026-10-10

- Toolchain: Go `1.26.0`, Windows amd64.
- Formatting: `gofmt` applied to the bootstrap.
- Static check: `go vet ./...` passed.
- Compilation: `go build ./...` and `go build -o bin/bookledger.exe ./cmd/server` passed.
- Runtime: the compiled executable was launched locally. `GET /health` returned HTTP 200 with JSON `{"status":"ok"}` and `Content-Type: application/json`; `/` and `/books` returned 404; `POST /health` returned 405.
- Invalid configuration: an address without a port caused startup to log an error and exit non-zero.
- Shutdown observation: Ctrl+C caused the bootstrap to log its shutdown message. Draining in-flight requests to the deadline was not separately tested.
- Scope: process scaffolding only. No schema, MySQL connection, business operation, benchmark, or business test is verified by these checks. Interactive VS Code debugging remains unverified.
- Next task: the maintainer runs the Go scaffold and begins the foundational Go and SQL exercises.

## Learning entry template

- Date and milestone:
- Goal and files authored:
- Toolchain and MySQL server versions:
- Prerequisites and fixture:
- Expected result:
- Actual result:
- Failure case tested:
- Explanation in the maintainer's own words:
- Limits and remaining questions:
- Next task:

For concurrency, record the action order in each connection. For optimization, record dataset size/distribution, query plans, timing conditions, and measured results. Do not substitute a successful build for business verification.
