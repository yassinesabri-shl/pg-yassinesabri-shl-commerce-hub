---
name: ADR-112
description: The orders service sends every order email itself.
globs: ["cmd/**","internal/**"]
alwaysApply: false
kind: adr
status: Deprecated
owner: Platform architect
revision: 1
origin: https://shl.atlassian.net/wiki/spaces/~71202058c67a3fe34f4165a8b8c49dc509cd2f/pages/474875241/ADR-112+We+send+order+emails+from+the+orders+service (Confluence page 474875241)
---

# ADR-112: We send order emails from the orders service

## Decision

The orders service sends every order email itself.

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
