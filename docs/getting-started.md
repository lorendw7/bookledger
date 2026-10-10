# Getting started

## Tools and roles

Go is the language and toolchain used to build this server. MySQL is a separate database server. SQL is the language used to define and query database data. VS Code edits repository files; MySQL Workbench or the `mysql` client sends SQL to MySQL.

This scaffold uses only Go's standard library. No database driver or third-party web framework is installed. The project module is `github.com/lorendw7/bookledger`.

## Check Go and run the server

From the repository root in PowerShell:

```powershell
go version
go run ./cmd/server
```

The observed local version is `go1.26.0 windows/amd64`; the module requires Go 1.26 or newer. Record your actual version if it differs. There is no separate package installation step for this scaffold.

Open `http://127.0.0.1:8080/health`, or use another terminal:

```powershell
Invoke-RestMethod http://127.0.0.1:8080/health
```

Expected JSON is `{"status":"ok"}`. `/books` and `/` are not implemented and return 404. `POST /health` returns 405. The health endpoint reports process availability only; it does not connect to MySQL.

Stop the server with Ctrl+C. The bootstrap requests graceful shutdown with a five-second deadline. See [the progress log](progress.md) for what was actually exercised.

## Address configuration

The default address is `127.0.0.1:8080`. To change it for the current terminal:

```powershell
$env:HTTP_ADDR = '127.0.0.1:8081'
go run ./cmd/server
```

After stopping the server, clear the override with `Remove-Item Env:HTTP_ADDR`. Go does not automatically read `.env` files in this project. Set environment variables directly; later database credentials must remain outside tracked files.

## Build and inspect

```powershell
go fmt ./...
go vet ./...
go build ./...
New-Item -ItemType Directory -Force bin
go build -o bin/bookledger.exe ./cmd/server
.\bin\bookledger.exe
```

The executable name above is for Windows. `bin/` is ignored. Formatting, vetting, and compilation do not verify bookstore behavior. Add maintainer-authored tests as implementation grows.

In VS Code, install the recommended Go extension. Formatting uses Go tooling. F5 uses the included launch configuration; it requires the extension's debug tools, including Delve. Stop any server using the same address before debugging. Interactive debugger setup has not been verified unless recorded in the progress log.

## Connect to MySQL separately

Use your configured local account and port:

```powershell
mysql -h 127.0.0.1 -P 3306 -u root -p
```

Enter the password at the prompt. If the command is unavailable, the initial Windows installation used:

```powershell
& 'C:\Program Files\MySQL\MySQL Server 8.0\bin\mysql.exe' -h 127.0.0.1 -P 3306 -u root -p
```

At the `mysql>` prompt, run these generic diagnostics:

```sql
SELECT 1;
SELECT VERSION();
SELECT DATABASE();
```

The client version and connected server version are different facts. The maintainer previously demonstrated server `8.0.45`; verify your current connection. `DATABASE()` can return `NULL` before selecting a database. A later application must use a dedicated limited account rather than an administrator account.

No schema scripts are included in this clean starting point. Write them using [SQL foundations](lessons/02-sql-foundations.md); removing repository files does not reset an existing MySQL database.

## Troubleshooting

| Symptom | Next action |
| --- | --- |
| Address already in use | Stop the other server or set another `HTTP_ADDR` |
| Invalid listen address | Use a valid `host:port` value |
| Go command unavailable | Check Go installation and reopen the terminal |
| MySQL access denied | Check the configured account, password, and connection host |
| MySQL connection refused | Check the service, host, and port |
| `go run` exits after Ctrl+C | Start it again when needed; no automatic restart tool is configured |

## Official references

- [Go module layout](https://go.dev/doc/modules/layout)
- [Go HTTP server](https://pkg.go.dev/net/http)
- [VS Code Go extension](https://marketplace.visualstudio.com/items?itemName=golang.Go)
- [MySQL connection tutorial](https://dev.mysql.com/doc/refman/8.0/en/connecting-disconnecting.html)
