# BookLedger

A Go and MySQL learning project for a small bookstore backend.

Build a catalog and an order system while learning SQL, HTTP APIs, transactions, concurrency, and service operation. The maintainer writes the core implementation; the assistant supplies non-business scaffolding and English learning documentation.

## Current status

The repository contains a standard-library Go HTTP scaffold with process health, request timeouts, environment-based address configuration, and graceful shutdown. There is no database connection, schema, catalog API, order logic, or executable business test yet. Those features are planned, not implemented.

Local environment: Go `1.26.0` on Windows; the maintainer previously demonstrated MySQL server `8.0.45` in Workbench. Current verification evidence belongs in [the progress log](docs/progress.md).

Formatting, static checks, compilation, health responses, route rejection, and invalid-address startup behavior were verified locally on 2026-10-10. Business milestones remain unfinished.

## Quick start

Install Go 1.26 or newer. From the repository root:

```powershell
go run ./cmd/server
```

In another terminal:

```powershell
Invoke-RestMethod http://127.0.0.1:8080/health
```

Expected response: `{"status":"ok"}`. This checks the HTTP process, not MySQL. Stop the server with Ctrl+C. To choose a different address, set `$env:HTTP_ADDR = '127.0.0.1:8081'` before starting it. See [Getting started](docs/getting-started.md) for build and editor setup.

## Learning path

1. Run the scaffold and read [Go foundations](docs/lessons/01-go-foundations.md).
2. Connect to MySQL and complete [SQL foundations](docs/lessons/02-sql-foundations.md).
3. Work through the [10-14 day preparation plan](docs/roadmap.md).
4. Implement and verify the [requirements](docs/requirements.md), recording actual results.

The plan combines project work, algorithms, and technical explanation practice. It is a preparation schedule, not a claim of production experience or completed features.

## Planned capabilities

- Book catalog, customer records, and order history.
- Transactional order creation and cancellation with consistent stock.
- Duplicate-request handling and concurrency verification.
- Query-plan analysis and measured index experiments.
- Basic packaging, configuration, and operational checks.

Payment is simulated. Use fictional data. A frontend is optional.

## Repository layout

```text
cmd/server/       HTTP server bootstrap and process health
internal/         Future maintainer-authored application packages
sql/              Future maintainer-authored SQL scripts
tests/            Verification guidance and future business tests
docs/             Setup, lessons, requirements, design, and evidence
go.mod            Go module; no third-party dependencies yet
AGENTS.md         Collaboration boundaries
LICENSE           MIT License
```

## Documentation

- [Getting started](docs/getting-started.md)
- [Roadmap and interview preparation](docs/roadmap.md)
- [Requirements and acceptance scenarios](docs/requirements.md)
- [Database and application design proposal](docs/database-design.md)
- [Progress and verification](docs/progress.md)
- [Future showcase](docs/showcase.md)
- [Contribution guide](CONTRIBUTING.md)

## License

Released under the [MIT License](LICENSE), copyright 2026 lorendw7.
