# SHOP-1 — Filter the weekly menu by diet in the catalogue

Key: SHOP-1
Repository: pg-yassinesabri-shl-catalogue-api
Context: std-http-apis@a50f7b53a8e0:docs/standards/std-http-apis.md, std-php-services@e55e59113305:docs/standards/std-php-services.md, pg-yassinesabri-shl-catalogue-api.ADR-001@368f280f41fb:pg-yassinesabri-shl-catalogue-api:decisions/ADR-001-catalogue-is-read-only-files.md
Hub commit: de02dec97968a7b0f36447a8dff54cae73314f30
Tracker key: not created — the playground estate has no tracker, so the second invocation of
`/decompose` has not run. A real run writes the tracker's own reference here.

## Traceability

Derives from: `docs/requirements/dietary-filter/requirements.md` § REQ-1 — A customer can show only the recipes that suit one diet L62-75
Derives from: `docs/requirements/dietary-filter/requirements.md` § REQ-2 — A diet the shop does not offer is refused, never ignored L77-88

Read in the repository, at one pinned commit, through `scripts/read-spoke.mjs`:

- `pg-yassinesabri-shl-catalogue-api@bd5786786131:src/Http/MenuController.php L19-36` — `show`, the one handler of `GET /v1/menus/{week}`
- `pg-yassinesabri-shl-catalogue-api@bd5786786131:data/recipes.json L3-8` — the six recipes and their `diet` tags
- `pg-yassinesabri-shl-catalogue-api@bd5786786131:tests/MenuEndpointsTest.php L14-25` — the published-week test this change must leave passing

## Acceptance criteria

| ID | Criterion | Type | Carries | Source |
|---|---|---|---|---|
| AC-1 | `GET /v1/menus/2026-W43?diet=vegetarian` answers 200 with exactly the recipes of that menu whose `diet` contains `vegetarian`, a recipe tagged `vegan` and `vegetarian` included | positive | REQ-1.AC-1 | requirements § REQ-1 L71; `pg-yassinesabri-shl-catalogue-api@bd5786786131:data/recipes.json L3-8` |
| AC-2 | `GET /v1/menus/2026-W43?diet=vegan` answers 200 with exactly the recipes of that menu whose `diet` contains `vegan` | positive | REQ-1.AC-2 | requirements § REQ-1 L72 |
| AC-3 | A filtered menu lists its recipes in the menu's own order | positive | REQ-1.AC-4 | requirements § REQ-1 L74; `pg-yassinesabri-shl-catalogue-api@bd5786786131:src/Http/MenuController.php L29-34` |
| AC-4 | `GET /v1/menus/2026-W43?diet=keto` answers 400 with the error code `unknown_diet` and no `recipes` field, as std-http-apis.05 and std-http-apis.04 require | negative | REQ-2.AC-1 | requirements § REQ-2 L87 |
| AC-5 | Each recipe in a filtered menu is byte-identical to the same recipe in the unfiltered menu | negative | REQ-1.AC-5 | requirements § REQ-1 L75 |
| AC-6 | The 400 answer's message does not contain the value sent: a marker sent as the diet appears nowhere in the response | negative | REQ-2.AC-2 | requirements § REQ-2 L88 |

The diets the endpoint accepts are `vegetarian` and `vegan`. The data is read from the files, as
pg-yassinesabri-shl-catalogue-api.ADR-001 decides, so the filter adds no store. Each criterion is a PHPUnit test that
sends a request through the application, as std-php-services.05 requires, under `/v1/`, as
std-http-apis.01 requires.

## Dependencies

SHOP-2 depends on this item (record D-2). This item depends on nothing.

## Decisions

| # | Interpretation | Why it is defensible | Confidence | Source |
|---|---|---|---|---|
| D-1 | The diet is a query parameter, `diet`, on the existing menu endpoint | A filter narrows a resource rather than naming a new one, and std-http-apis.01 keeps the version first in the path | high | std-http-apis § Must |
| D-2 | An empty filtered menu answers 200 with an empty `recipes` array | A known diet with no recipe this week is not an error; REQ-2 is about an unknown diet | high | requirements § REQ-2 L77-88 |

## Clarifications

NONE
