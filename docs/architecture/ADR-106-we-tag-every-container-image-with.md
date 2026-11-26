---
name: ADR-106
description: We tag every container image with the commit it was built from.
globs: ["**/Dockerfile"]
alwaysApply: false
kind: adr
status: Accepted
owner: Lead architect (Ada Author)
revision: 1
origin: https://shl.atlassian.net/wiki/spaces/~71202058c67a3fe34f4165a8b8c49dc509cd2f/pages/474842661/ADR-106+We+tag+every+container+image+with+its+commit (Confluence page 474842661)
---

# ADR-106: We tag every container image with its commit

## Decision

We tag every container image with the commit it was built from.

## Rules

- MUST use Postgres for a new relational store.
- MUST NOT share a schema between two domains.

## Why

None.

## Rejected

- Not keep every engine, because three sets of backups to run.
- Not MySQL everywhere, because no team runs it today.

## Accepted costs

- One backup design for the estate.
