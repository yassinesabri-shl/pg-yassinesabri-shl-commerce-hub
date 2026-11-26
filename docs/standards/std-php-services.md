---
name: std-php-services
description: How a PHP HTTP service in the commerce estate declares types, depends on packages, handles a request and is tested.
globs: ["src/**/*.php", "public/**/*.php", "tests/**/*.php"]
alwaysApply: false
kind: standard
status: Active
owner: backend lead
revision: v1, 2026-09-28
origin: the Larder engineering handbook, page "PHP services", section PHP
---

# std-php-services: PHP HTTP services

## Applies to

Every PHP file of an HTTP service under `src/`, `public/` and `tests/`. It does not cover the
shape of a response, which std-http-apis governs.

## Must

- **std-php-services.01** MUST open every PHP file with `declare(strict_types=1);`. *(Source: PHP-1)*
- **std-php-services.02** MUST declare a parameter type and a return type on every function and method. *(Source: PHP-2)*
- **std-php-services.03** MUST load classes through Composer's PSR-4 autoloader, and MUST NOT use `require` or `include` outside `public/index.php`. *(Source: PHP-3)*
- **std-php-services.04** MUST NOT add a Composer package to `require` unless a decision record allows it. A package in `require-dev` needs no record. *(Source: PHP-4)*
- **std-php-services.05** MUST cover each acceptance criterion with a PHPUnit test that sends a request through the application object and reads the response. *(Source: PHP-5)*

## Should

- **std-php-services.06** SHOULD make a class `final` unless a test or a decision record needs a subclass. *(Source: PHP-6)*

## Values

| Value | Setting | Applies to | Source |
|---|---|---|---|
| The lowest PHP version a service supports | 8.3 | std-php-services.01 | PHP-1 |

## Checked by

- **std-php-services.01** — LINT_COMMAND: PHP-CS-Fixer, rule `declare_strict_types`.
- **std-php-services.02** — TYPECHECK_COMMAND: PHPStan at level 8.
- **std-php-services.03** — review: no `require` or `include` outside `public/index.php`.
- **std-php-services.04** — review: each new `require` entry in `composer.json` names its record.
- **std-php-services.05** — review: the test builds the application and calls `handle`.
- **std-php-services.06** — review.

## Relations

- Defers to: ADR-001, for the integer type of an amount. ADR-002, for the request id.

## Exceptions

The backend lead grants an exception, and the design that needs it records it in its decisions log.

## Unresolved

None.

## Origin

The Larder engineering handbook, page "PHP services", section PHP, v1 of 2026-09-28. This summary
leaves out the editor settings, which each service's `checks.env` makes a command.
