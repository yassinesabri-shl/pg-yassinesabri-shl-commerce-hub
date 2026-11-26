---
name: ADR-001
description: Every amount of money in the commerce estate is an integer count of the currency's minor unit, carried with its ISO 4217 currency code, and never a float.
globs: ["**/*"]
alwaysApply: true
kind: adr
status: Accepted
owner: lead architect
revision: v1, 2026-10-20
origin: the Larder architecture decision log, record C-001, "Money in minor units"
---

# ADR-001: Money is an integer count of minor units, with its currency

## Decision

Every amount of money is an integer count of the currency's minor unit, carried beside its ISO 4217 currency code, in every system and on every wire.

## Rules

- MUST carry an amount as the JSON object `{"amount_minor": <integer>, "currency": "<ISO 4217 code>"}`.
- MUST store and compute an amount as an integer type: `int64` in Go, `int` in PHP, `long` in Java, `number` checked with `Number.isSafeInteger` in TypeScript.
- MUST NOT use a floating-point type for an amount at any point, including an intermediate result.
- MUST NOT add two amounts whose currencies differ. Such a call is an error, not a conversion.
- MUST convert an amount to a display string only at the edge that shows it to a person, with the currency's own number of minor-unit digits.

## Why

The first prototype stored prices as floats, and a basket of three recipes at 7.30 summed to 21.899999999999998.
The finance team reconciles orders to the cent. Source: the Larder pricing incident review of 2026-09-14.

## Rejected

- Not a decimal string such as `"7.30"`, because each language parses it into a different type, and the PHP prototype parsed it into a float.
- Not a decimal library in each service, because the estate has four languages and no library is common to them.

## Accepted costs

- A currency with three minor-unit digits, such as BHD, needs its digit count in the display code. Larder sells only in GBP and EUR today.
