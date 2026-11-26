---
name: std-http-apis
description: The URL, status code, error body and versioning rules every HTTP API in the commerce estate follows, whatever its language.
globs: ["src/**/*.php", "public/**/*.php", "cmd/**/*.go", "internal/**/*.go", "app/api/**"]
alwaysApply: false
kind: standard
status: Active
owner: lead architect
revision: v2, 2026-10-12
origin: the Larder engineering handbook, page "HTTP APIs", section API
---

# std-http-apis: HTTP APIs

## Applies to

Every HTTP endpoint a commerce service serves, in any language, and the tests that call it. It
does not cover the storefront's pages, which serve HTML to a browser, or a service's internal
function calls.

## Must

- **std-http-apis.01** MUST put the major version first in every path, as `/v1/...`. *(Source: API-1)*
- **std-http-apis.02** MUST name a path segment as a plural noun in kebab case, such as `/v1/pick-lists`. *(Source: API-2)*
- **std-http-apis.03** MUST name a JSON field in snake case. *(Source: API-3)*
- **std-http-apis.04** MUST answer an error with the body `{"error": {"code": "<snake_case>", "message": "<sentence>"}}`. *(Source: API-4)*
- **std-http-apis.05** MUST answer 400 for a body or a parameter that fails validation, 404 for an unknown resource, 405 with an `Allow` header for a wrong method, and 409 for a state conflict. *(Source: API-5)*
- **std-http-apis.06** MUST NOT put a stack trace, an exception message or a file path in a response. *(Source: API-6)*
- **std-http-apis.07** MUST NOT remove a field or change its type within one major version. *(Source: API-7)*

## Should

- **std-http-apis.08** SHOULD answer a collection as an object with one named array, such as `{"recipes": [...]}`, and not as a bare array. *(Source: API-8)*

## Values

| Value | Setting | Applies to | Source |
|---|---|---|---|
| The largest request body a service accepts | 64 KiB | std-http-apis.05 | API-5 |

## Checked by

- **std-http-apis.01** — review: every route in the diff starts with `/v<n>/`.
- **std-http-apis.02** — review: each new path segment is plural and kebab case.
- **std-http-apis.03** — review: each new JSON field is snake case.
- **std-http-apis.04** — review: a negative test asserts the error body's two fields.
- **std-http-apis.05** — review: a negative test for each status the endpoint can return.
- **std-http-apis.06** — review: the 500 handler writes a fixed message.
- **std-http-apis.07** — review: the diff removes or retypes no field of a released response.
- **std-http-apis.08** — review: the collection response has one named array.

## Relations

- Defers to: ADR-001, for the shape of an amount. ADR-002, for the request id header.

## Exceptions

The lead architect grants an exception, and the design that needs it records it in its decisions log.

## Unresolved

- UNRESOLVED — whether a list endpoint pages its results, and the page size. Owner: lead architect. Resolves: the first list that returns more than 100 items.

## Origin

The Larder engineering handbook, page "HTTP APIs", section API, v2 of 2026-10-12. This summary
leaves out the OpenAPI style guide, which each service's contracts folder carries.
