---
name: ADR-108
description: Every service exposes a health endpoint at /health that answers within one second.
globs: ["src/**","cmd/**"]
alwaysApply: false
kind: adr
status: Superseded by ADR-101
owner: Platform architect
revision: 1
origin: https://shl.atlassian.net/wiki/spaces/~71202058c67a3fe34f4165a8b8c49dc509cd2f/pages/474875201/ADR-108+Every+service+exposes+a+health+endpoint (Confluence page 474875201)
---

# ADR-108: Every service exposes a health endpoint

## Decision

Every service exposes a health endpoint at /health that answers within one second.

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
