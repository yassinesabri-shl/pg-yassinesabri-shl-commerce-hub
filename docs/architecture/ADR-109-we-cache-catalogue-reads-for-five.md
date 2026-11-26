---
name: ADR-109
description: We cache catalogue reads for five minutes at the gateway.
globs: ["src/**"]
alwaysApply: false
kind: adr
status: Accepted
owner: Platform architect
revision: 1
origin: https://shl.atlassian.net/wiki/spaces/~71202058c67a3fe34f4165a8b8c49dc509cd2f/pages/474875221/ADR-109+We+cache+catalogue+reads+for+five+minutes (Confluence page 474875221)
---

# ADR-109: We cache catalogue reads for five minutes

## Decision

We cache catalogue reads for five minutes at the gateway.

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
