# Decomposition — dietary-filter

| Field | Value |
|---|---|
| Source | `docs/requirements/dietary-filter/requirements.md` |
| Source revision | r1, merged 2026-10-20 with `check-requirements.js` green; REQ-4 held on CLAR-SHOP-diet-01 |
| Record revision | r1 |
| Date | 2026-10-20 |
| Key block | SHOP-1 to SHOP-2, taken from `docs/backlog/keys.json`; `next` moved to 3 in the same pull request |
| Review | `dietary-filter.decomposition-review.md`, beside this record — the critic's final round, bound to this record's content hash |

## Coverage map

| Source section | Lines | Items | Disposition | Reason and owner |
|---|---|---|---|---|
| REQ-1 — show only the recipes that suit one diet | L62-75 | SHOP-1 (AC-1, AC-2, AC-3, AC-5 carry REQ-1.AC-1, AC-2, AC-4, AC-5), SHOP-2 (AC-3 carries REQ-1.AC-3) | Covered | The catalogue filters and keeps the order; the storefront offers the choice and the way back to the full menu |
| REQ-2 — an unknown diet is refused | L77-88 | SHOP-1 (AC-4 carries REQ-2.AC-1, AC-6 carries REQ-2.AC-2) | Covered | The catalogue refuses; the storefront shows the refusal it receives through SHOP-2 AC-4, which carries REQ-2.AC-1 on the page |
| REQ-3 — the chosen diet survives a reload and a link | L90-97 | SHOP-2 (AC-1, AC-2 carry REQ-3.AC-1, AC-2) | Covered | The storefront keeps the diet in the page's address |
| REQ-4 — gluten-free, certified only | L99-108 | none yet, blocked | Unresolved | UNRESOLVED — who certifies a recipe as gluten-free, and how the certification reaches the catalogue (CLAR-SHOP-diet-01, blocking). Owner: food safety lead. Resolves: the clarification closes and REQ-4 is cut in a new revision of this record, from a new block; no key is minted until then. |
| §7 Constraints | L110-114 | SHOP-1 | Covered | REQ-1.AC-5 made observable as SHOP-1 AC-5 |
| §3 Scope — out of scope | L42-44 | deliberately none | Out of scope | Two diets at once, and allergen information, excluded by the source; head of product |
| §2 Purpose and business outcome | L23-30 | deliberately none | Out of scope | The situation and the outcome, not a requirement; requirements author |
| §4 Definitions | L46-51 | deliberately none | Out of scope | Terms the criteria use; requirements author |
| §5 Parties | L53-58 | deliberately none | Out of scope | The roles the clarification routes to; requirements author |
| §9 CLAR-SHOP-diet-01 | L136 | none yet, blocked | Unresolved | UNRESOLVED — who certifies a recipe as gluten-free, and how the certification reaches the catalogue. Owner: food safety lead. Resolves: CLAR-SHOP-diet-01 closes and REQ-4 is cut from a new block. |
| §10 Assumptions A-1 and A-2 | L142-143 | SHOP-1, SHOP-2 | Covered | A-1 is the week SHOP-2 asks for; A-2 is SHOP-1 AC-1 |
| §1 Document control and §8 Coverage map | L3-21, L116-130 | deliberately none | Out of scope | Document metadata and the document's own map; requirements author |

## Repository map

One row per repository the hub lists. `Read at` is the trunk commit the row's evidence came from,
as `scripts/read-spoke.mjs` printed it.

| Repository | Read at | Disposition | Stories, or the evidence read |
|---|---|---|---|
| `pg-yassinesabri-shl-catalogue-api` | `bd5786786131` | Changes | SHOP-1. The menu endpoint is `pg-yassinesabri-shl-catalogue-api@bd5786786131:src/Http/MenuController.php L19-36`, which answers every recipe of the week in the menu's order and reads no query parameter; the diet tags are already on each recipe, `pg-yassinesabri-shl-catalogue-api@bd5786786131:data/recipes.json L3-8` |
| `pg-yassinesabri-shl-storefront-web` | `68f5dffe4f2c` | Changes | SHOP-2. The menu page is `pg-yassinesabri-shl-storefront-web@68f5dffe4f2c:app/page.tsx L9-17`, which asks `getMenu` for the current week, `pg-yassinesabri-shl-storefront-web@68f5dffe4f2c:lib/catalogue.ts L34-49`; neither takes a diet |
| `pg-yassinesabri-shl-orders-api` | `14070b378bfa` | No change | An order carries recipe ids and frozen prices, `pg-yassinesabri-shl-orders-api@14070b378bfa:internal/httpapi/wire.go L28-38`, and no diet; a filtered menu changes nothing a customer orders |

## Items

| Key | Title | Repository | Carries |
|---|---|---|---|
| SHOP-1 | Filter the weekly menu by diet in the catalogue | `pg-yassinesabri-shl-catalogue-api` | REQ-1.AC-1, REQ-1.AC-2, REQ-1.AC-4, REQ-1.AC-5, REQ-2.AC-1, REQ-2.AC-2 |
| SHOP-2 | Offer the diet filter on the menu page and keep it in the address | `pg-yassinesabri-shl-storefront-web` | REQ-3.AC-1, REQ-3.AC-2, REQ-1.AC-3, REQ-2.AC-1 |

## Dependency map

| From | To | Type | Why |
|---|---|---|---|
| SHOP-2 | SHOP-1 | blocks | The page asks the catalogue for a filtered menu; until the catalogue reads the diet, the storefront has nothing to show (D-2) |

Acyclic: one edge.

## Decisions

| # | Decision | Alternatives rejected | Why | Date |
|---|---|---|---|---|
| D-1 | The catalogue filters, and the storefront asks for the filtered menu | The storefront fetches the full menu and filters it on the server | The refusal of an unknown diet is the catalogue's to give under std-http-apis, and one place owns the list of diets | 2026-10-20 |
| D-2 | SHOP-2 depends on SHOP-1 | No edge, with the storefront filtering until the catalogue is ready | A storefront filter would be a second implementation of the same rule, removed once SHOP-1 ships | 2026-10-20 |

## Clarifications

| ID | Question | Source | Blocking | Routed to | Status | Resolution | Resolved |
|---|---|---|---|---|---|---|---|
| CLAR-SHOP-diet-02 | Should the diet list the storefront offers come from the catalogue, or stay fixed at vegetarian and vegan in the storefront? Not blocking: SHOP-2 offers the two the requirements name, and the catalogue refuses any other | requirements § REQ-1 L62-75; `pg-yassinesabri-shl-storefront-web@68f5dffe4f2c:lib/catalogue.ts L34-49` | no | Head of product | Open |  |  |
