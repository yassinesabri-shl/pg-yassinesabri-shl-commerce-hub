---
name: std-eng-py
description: How every public API names its eng-py.
globs: ["**/*.py"]
alwaysApply: false
kind: standard
status: Active
owner: Lead architect
revision: 2
origin: https://shl.atlassian.net/wiki/spaces/~71202058c67a3fe34f4165a8b8c49dc509cd2f/pages/474809895/std-eng-py+Python (Confluence page 474809895)
---

# std-eng-py: Python

## Applies to

Every public HTTP API. Internal events are not covered.

## Must

- **std-eng-py.01** MUST use kebab-case in a path segment.
- **std-eng-py.02** MUST NOT put a verb in a path.

## Should

- **std-eng-py.03** SHOULD keep a path under five segments.

## Values

| Value | Setting | Applies to | Source |
| --- | --- | --- | --- |
| Path segments | 5 at most | All public APIs | API guide, page 2 |

## Checked by

- std-eng-py.01 — review: the reviewer reads every new path.

## Relations

None.

## Exceptions

- Granted by: Lead architect

## Unresolved

None.

## Origin

- Source: API guide v2, the API guild space
