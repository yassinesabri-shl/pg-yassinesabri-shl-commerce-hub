---
name: ADR-110
description: We keep storefront sessions in signed cookies, never in server memory.
globs: ["app/**"]
alwaysApply: false
kind: adr
status: Accepted
owner: Platform architect
revision: 1
origin: https://shl.atlassian.net/wiki/spaces/~71202058c67a3fe34f4165a8b8c49dc509cd2f/pages/474678726/ADR-110+We+keep+sessions+in+signed+cookies (Confluence page 474678726)
---

# ADR-110: We keep sessions in signed cookies

## Decision

We keep storefront sessions in signed cookies, never in server memory.

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
