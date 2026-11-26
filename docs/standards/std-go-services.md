---
name: std-go-services
description: How a Go HTTP service in the commerce estate is laid out, depends on modules, handles errors and is tested.
globs: ["**/*.go", "go.mod"]
alwaysApply: false
kind: standard
status: Active
owner: backend lead
revision: v1, 2026-09-28
origin: the Larder engineering handbook, page "Go services", section GO
---

# std-go-services: Go HTTP services

## Applies to

Every Go file and the `go.mod` of an HTTP service, its tests included. It does not cover the
shape of a response, which std-http-apis governs.

## Must

- **std-go-services.01** MUST keep the entry point in `cmd/<service>/main.go`, and every other package under `internal/`. *(Source: GO-1)*
- **std-go-services.02** MUST NOT add a module to `go.mod` outside the standard library unless a decision record allows it. *(Source: GO-2)*
- **std-go-services.03** MUST return an error to the caller, wrapped with `fmt.Errorf("...: %w", err)`, and MUST NOT call `panic` outside `main`. *(Source: GO-3)*
- **std-go-services.04** MUST cover each acceptance criterion with a test that calls the handler through `net/http/httptest`. *(Source: GO-4)*
- **std-go-services.05** MUST format every file with `gofmt`. *(Source: GO-5)*

## Should

- **std-go-services.06** SHOULD write a test with several cases as a table of named cases. *(Source: GO-6)*

## Values

| Value | Setting | Applies to | Source |
|---|---|---|---|
| The lowest Go version a service supports | 1.23 | std-go-services.02 | GO-2 |

## Checked by

- **std-go-services.01** — review: the diff adds no package outside `cmd/` and `internal/`.
- **std-go-services.02** — review: each new `require` line in `go.mod` names its record.
- **std-go-services.03** — LINT_COMMAND: `go vet`, and review for `panic`.
- **std-go-services.04** — review: each criterion's test uses `httptest`.
- **std-go-services.05** — FORMAT_COMMAND: `gofmt -l`.
- **std-go-services.06** — review.

## Relations

- Defers to: ADR-001, for the integer type of an amount. ADR-002, for the request id.
- Settled on ingest: the operations hub also keeps a Go standard, for timeouts and contexts. The two govern different topics and do not conflict. Answer given by the lead architect, 2026-10-20.

## Exceptions

The backend lead grants an exception, and the design that needs it records it in its decisions log.

## Unresolved

None.

## Origin

The Larder engineering handbook, page "Go services", section GO, v1 of 2026-09-28. This summary
leaves out the module proxy settings, which belong to the build machines.
