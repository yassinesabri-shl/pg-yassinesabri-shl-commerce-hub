---
name: std-nextjs-web
description: How the Next.js storefront renders pages, calls the commerce services, handles a customer's input and is tested.
globs: ["app/**", "components/**", "lib/**"]
alwaysApply: false
kind: standard
status: Active
owner: frontend lead
revision: v1, 2026-10-05
origin: the Larder engineering handbook, page "Web front ends", section WEB
---

# std-nextjs-web: Next.js web front ends

## Applies to

Every TypeScript and TSX file of a Next.js App Router application under `app/`, `components/`
and `lib/`, its tests included. It does not cover the HTTP APIs the application calls, which
std-http-apis governs.

## Must

- **std-nextjs-web.01** MUST call a commerce service only from server code: a server component, a server action or a route handler. *(Source: WEB-1)*
- **std-nextjs-web.02** MUST read a service's base URL from `process.env` in server code, and MUST NOT expose it through a `NEXT_PUBLIC_` variable. *(Source: WEB-2)*
- **std-nextjs-web.03** MUST validate every value of a form or a URL parameter in server code before the value is sent to a service. *(Source: WEB-3)*
- **std-nextjs-web.04** MUST mark a component `"use client"` only when it uses state, an effect or a browser event. *(Source: WEB-4)*
- **std-nextjs-web.05** MUST show the `x-request-id` of a failed service call on the error the customer sees. *(Source: WEB-5)*
- **std-nextjs-web.06** MUST cover each acceptance criterion with a Vitest test, and MUST replace each service with a fake `fetch` in that test. *(Source: WEB-6)*

## Should

- **std-nextjs-web.07** SHOULD keep each call to a service in one function in `lib/`, so that a page does not build a URL. *(Source: WEB-7)*

## Values

| Value | Setting | Applies to | Source |
|---|---|---|---|
| The time a server call to a service waits before it fails | 3 seconds | std-nextjs-web.01 | WEB-1 |

## Checked by

- **std-nextjs-web.01** — review: no `fetch` to a service URL in a file marked `"use client"`.
- **std-nextjs-web.02** — review: no `NEXT_PUBLIC_` variable names a service.
- **std-nextjs-web.03** — review: a negative test sends an invalid value for each field.
- **std-nextjs-web.04** — LINT_COMMAND: ESLint with the Next.js rules, and review.
- **std-nextjs-web.05** — review: a test asserts that the error shows the id.
- **std-nextjs-web.06** — TEST_COMMAND: Vitest, and review of the test names.
- **std-nextjs-web.07** — review: the page imports a function from `lib/`.

## Relations

- Defers to: ADR-001, for the display of an amount. ADR-002, for the request id.

## Exceptions

The frontend lead grants an exception, and the design that needs it records it in its decisions log.

## Unresolved

- UNRESOLVED — whether the storefront needs an end-to-end browser test, and with which tool. Owner: frontend lead. Resolves: the first story that changes the checkout flow.

## Origin

The Larder engineering handbook, page "Web front ends", section WEB, v1 of 2026-10-05. This
summary leaves out the design system's tokens, which the storefront's rules carry.
