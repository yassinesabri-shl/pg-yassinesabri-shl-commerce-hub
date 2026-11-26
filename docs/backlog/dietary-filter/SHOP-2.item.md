# SHOP-2 — Offer the diet filter on the menu page and keep it in the address

Key: SHOP-2
Repository: pg-yassinesabri-shl-storefront-web
Context: ADR-003@ba777a78da7a:docs/architecture/ADR-003-services-share-no-database.md, std-nextjs-web@ebb3fe946f94:docs/standards/std-nextjs-web.md
Hub commit: de02dec97968a7b0f36447a8dff54cae73314f30
Tracker key: not created — the playground estate has no tracker, so the second invocation of
`/decompose` has not run. A real run writes the tracker's own reference here.

## Traceability

Derives from: `docs/requirements/dietary-filter/requirements.md` § REQ-3 — The chosen diet survives a reload and a shared link L90-97
Derives from: `docs/requirements/dietary-filter/requirements.md` § REQ-1 — A customer can show only the recipes that suit one diet L62-75
Derives from: `docs/requirements/dietary-filter/requirements.md` § REQ-2 — A diet the shop does not offer is refused, never ignored L77-88

Read in the repository, at one pinned commit, through `scripts/read-spoke.mjs`:

- `pg-yassinesabri-shl-storefront-web@68f5dffe4f2c:app/page.tsx L9-17` — `MenuPage`, the menu page
- `pg-yassinesabri-shl-storefront-web@68f5dffe4f2c:lib/catalogue.ts L34-49` — `getMenu`, the one call to the catalogue's menu endpoint
- `pg-yassinesabri-shl-storefront-web@68f5dffe4f2c:components/MenuList.tsx L4-15` — `MenuList`, which renders the recipes

## Acceptance criteria

| ID | Criterion | Type | Carries | Source |
|---|---|---|---|---|
| AC-1 | Choosing vegetarian or vegan on the menu page puts `?diet=<diet>` in the page's address | positive | REQ-3.AC-1 | requirements § REQ-3 L96 |
| AC-2 | Opening `/?diet=vegan` renders the menu the catalogue answers for `diet=vegan`, with no other step | positive | REQ-3.AC-2 | requirements § REQ-3 L97; `pg-yassinesabri-shl-storefront-web@68f5dffe4f2c:app/page.tsx L9-17` |
| AC-3 | The menu page offers a link to the full menu, `/` with no `diet`, which renders the unfiltered menu | positive | REQ-1.AC-3 | requirements § REQ-1 L73 |
| AC-4 | Opening `/?diet=keto` shows the message "That diet is not offered." and no recipes, and the page does not repeat the value | negative | REQ-2.AC-1 | requirements § REQ-2 L87 |

`getMenu` passes the diet to the catalogue in server code only, as std-nextjs-web.01 requires, and
validates it there first, as std-nextjs-web.03 requires. The storefront reads the catalogue only
through its API, as ADR-003 decides. Each criterion is a Vitest test with a fake `fetch`, as
std-nextjs-web.06 requires.

## Dependencies

Depends on SHOP-1: the catalogue must accept `diet` before the page can ask for it (record D-2).

## Decisions

| # | Interpretation | Why it is defensible | Confidence | Source |
|---|---|---|---|---|
| D-1 | The filter is two links, not a form | A link keeps the diet in the address with no client code, and std-nextjs-web.04 keeps a component a server component unless it needs state | high | std-nextjs-web § Must |

## Clarifications

NONE
