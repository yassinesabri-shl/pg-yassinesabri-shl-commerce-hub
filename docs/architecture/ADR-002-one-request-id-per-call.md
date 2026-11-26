---
name: ADR-002
description: Every call in the commerce estate carries one request id, x-request-id on HTTP, from the storefront to every service it reaches, set once and never rewritten.
globs: ["**/*"]
alwaysApply: true
kind: adr
status: Accepted
owner: lead architect
revision: v1, 2026-10-20
origin: the Larder architecture decision log, record C-002, "One request id per call"
---

# ADR-002: One request id names a call in every system it reaches

## Decision

Every call carries one request id in the HTTP header `x-request-id`, from the system that first sees the call to every system it reaches and every log line it writes.

## Rules

- MUST read `x-request-id` from an incoming request, and use it when it matches `^[A-Za-z0-9-]{8,64}$`.
- MUST generate a new UUID v4 when the header is missing or does not match that grammar.
- MUST send the id back in the `x-request-id` header of every response, an error response included.
- MUST pass the id unchanged in the `x-request-id` header of every outgoing call the request causes.
- MUST write the id as the field `request_id` in every log line about the request.
- MUST NOT add a second correlation header, such as `correlation-id` or `traceparent`.

## Why

A customer who reports a failed checkout quotes one value from the error page.
Support must find that value in the storefront, the catalogue and the orders logs.
Source: the Larder support handover of 2026-10-01.

## Rejected

- Not W3C `traceparent`, because no system in the estate runs a tracing agent, and a person must be able to read the id on an error page.

## Accepted costs

- A caller that sends a malformed id loses its own id, and gets a new one back. A service must not repair the value.
