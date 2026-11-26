---
name: ADR-101
description: We use Postgres for every new service that needs a relational store.
globs: ["services/orders/**","libs/db/**"]
alwaysApply: false
kind: adr
status: Accepted
owner: Platform architect
revision: 1
origin: https://shl.atlassian.net/wiki/spaces/~71202058c67a3fe34f4165a8b8c49dc509cd2f/pages/474809795/ADR-101+We+use+Postgres+for+every+new+relational+store (Confluence page 474809795)
---

# ADR-101: We use Postgres for every new relational store

## Decision

We use Postgres for every new service that needs a relational store.

## Rules

- MUST use Postgres for a new relational store.
- MUST NOT share a schema between two domains.

## Why

Each team picks its own database today.

## Rejected

- Not Keep every engine, because Three sets of backups to run.
- Not MySQL everywhere, because No team runs it today.

## Accepted costs

- One backup design for the estate.
