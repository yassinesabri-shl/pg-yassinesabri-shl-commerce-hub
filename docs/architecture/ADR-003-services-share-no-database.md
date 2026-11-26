---
name: ADR-003
description: Each commerce service owns its own data and reaches another service only through that service's HTTP API; no two services read or write one database.
globs: ["**/*"]
alwaysApply: true
kind: adr
status: Accepted
owner: lead architect
revision: v1, 2026-10-20
origin: the Larder architecture decision log, record C-003, "Services share no database"
---

# ADR-003: A service owns its data, and others reach it only through its API

## Decision

Each service owns its own data store, and another service reads or changes that data only through the owner's versioned HTTP API.

## Rules

- MUST read another service's data only through that service's HTTP API, at a base URL taken from configuration.
- MUST NOT open a connection to another service's data store, or read its files.
- MUST NOT copy another service's data into a store of your own, except a value frozen at a moment of business meaning, such as the price on an order.
- MUST read the base URL of every service a service calls from an environment variable named `<SERVICE>_URL`, such as `CATALOGUE_URL`.

## Why

Recipes, prices and orders change on different schedules and are owned by different teams.
A shared database couples their releases. Source: the Larder platform principles, principle 2, 2026-08-30.

## Rejected

- Not one shared PostgreSQL schema, because one team's migration would then need the other teams' sign-off.
- Not an event bus, because the estate has three services and no team to run a broker. Revisit when a fourth team joins.

## Accepted costs

- A page that shows recipes and an order makes two calls, not one join.
- An order keeps the price it was placed at, even when the catalogue changes the price later. This is on purpose.
