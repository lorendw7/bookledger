# Lesson 01: Go foundations and the HTTP scaffold

## Goal

Run the scaffold and explain its control flow before implementing bookstore behavior. Begin with [Getting started](../getting-started.md).

## Language, toolchain, and module

Go is a compiled language. The `go` command builds, runs, formats, and checks Go programs. `go.mod` identifies the module and required Go language/toolchain baseline. A package groups source files in a directory; `package main` with a `main` function defines an executable program.

Generic teaching example:

```go
package main

import "fmt"

func main() {
    label := "practice"
    count := 2
    fmt.Println(label, count)
}
```

Here `:=` declares and initializes local variables; their types are inferred. Go formatting is performed with `gofmt`. Keep scratch examples outside the server package so that a second `main` function does not conflict with it.

## Read the real bootstrap

Open `cmd/server/main.go` and trace these steps:

1. `main` calls `run` and reports a returned error.
2. `run` reads `HTTP_ADDR`, falling back to the local address.
3. `http.NewServeMux` creates the method/path router.
4. The health handler sends JSON using the response writer.
5. The HTTP server sets request timeouts and starts on a listener.
6. A signal requests shutdown; a context bounds the wait for active requests.

`http.ResponseWriter` writes the response; `*http.Request` provides request information. The pattern `GET /health` accepts GET and, by Go's routing rules, HEAD. It is process scaffolding, not a catalog API.

## Errors before concurrency

Go commonly returns an error alongside a result. Check errors before using the result. In the bootstrap, failure to listen is returned to `main` and produces a non-zero exit. Do not assume logging a failed business operation makes it successful.

A goroutine is a concurrently running function. The bootstrap uses one to serve HTTP while waiting for a shutdown signal. A channel communicates the serving result. Learn these mechanics from this small example before coordinating business state.

Context carries cancellation and deadlines. A deadline bounds waiting; it does not automatically undo a committed database operation. Later SQL transactions and request retry semantics must be designed separately.

## Exercises

- Run `/health` and identify the status, content type, and body.
- Explain why health can succeed while MySQL is unavailable.
- Change the address through the environment and restart the program.
- Explain the difference between an HTTP request timeout and transaction rollback.
- In a scratch program, practice a struct, a slice, a map, and a function returning an error.

Record observations in [the progress log](../progress.md). Do not add bookstore handlers until their requirements are understood.

## Official references

- [A Tour of Go](https://go.dev/tour/)
- [Go module layout](https://go.dev/doc/modules/layout)
- [HTTP package](https://pkg.go.dev/net/http)
- [Context package](https://pkg.go.dev/context)
