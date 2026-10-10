# Verification workspace

The maintainer will write executable business tests here or in Go `_test.go` files beside the packages they exercise. No executable business tests are supplied.

Begin with [the acceptance scenarios](../docs/requirements.md). Describe each fixture, prerequisite, expected result, actual result, and cleanup. Include rollback, last-copy contention, repeated cancellation, and duplicate requests as those features are implemented.

`go vet` and `go build` verify aspects of the scaffold; neither proves checkout correctness. A health response verifies the process only. Assistants may describe scenarios and review results under [AGENTS.md](../AGENTS.md).
