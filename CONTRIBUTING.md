# Contributing

BookLedger is a learning project. Keep changes focused on one observable behavior or one concept.

## Workflow

1. Choose a task from [the roadmap](docs/roadmap.md).
2. Create a focused branch. Assistant-created feature branches use `codex/`.
3. The maintainer writes core implementation and relevant business tests.
4. Run the behavior's acceptance scenarios, including failures.
5. Update English documentation and record results in [the progress log](docs/progress.md).
6. Review and commit a coherent change.

Follow [AGENTS.md](AGENTS.md) for implementation ownership. Assistants maintain non-business scaffolding and explanations.

## Go conventions

Use `gofmt`. Prefer the standard library until a dependency solves a concrete need. Return and handle errors; do not hide failed database or transaction operations. Introduce packages as responsibilities emerge rather than prebuilding every layer.

Typical scaffold checks:

```powershell
go fmt ./...
go vet ./...
go build ./...
```

Once maintainer-authored tests exist, run `go test ./...` as well. A command succeeding when no test files exist is not business verification.

## SQL and data

Use descriptive names and lowercase `snake_case` identifiers. Keep schema changes, fictional seed data, and experiments separate. Explain prerequisites, execution order, expected results, and rerun behavior for each script.

Use one documented currency. Keep credentials, dumps, generated binaries, and local configuration out of commits.

## Definition of done

- The intended behavior and relevant failures have been verified.
- Documentation accurately describes implementation and limitations.
- Actual versions and observed results are recorded.
- No local secrets or generated artifacts are included.
- License notices remain intact.
