---
name: ADR-113
description: We keep the first Decision sentence short.
globs: ["services/orders/**","libs/db/**"]
alwaysApply: false
kind: adr
status: Accepted
owner: Platform architect
revision: 2
origin: https://shl.atlassian.net/wiki/spaces/~71202058c67a3fe34f4165a8b8c49dc509cd2f/pages/474810094/ADR-113+A+Decision+whose+first+sentence+is+too+long (Confluence page 474810094)
---

# ADR-113: A Decision whose first sentence is too long

## Decision

We keep the first Decision sentence short.

## Rules

- MUST use Postgres for a new relational store.
- MUST NOT share a schema between two domains.

## Why

Each team picks its own database today.

## Rejected

- Not keep every engine, because three sets of backups to run.
- Not MySQL everywhere, because no team runs it today.

## Accepted costs

- One backup design for the estate.
