# Requirements — dietary filter: a customer can show only this week's recipes that suit their diet

## 1. Document control

| Field | Value |
|---|---|
| Document revision | r1 |
| Date | 2026-10-20 |
| Owning role | Head of product |
| Review | `requirements-review.md`, beside this document — the critic's final round, bound to this document's content hash; `check-requirements.js` reads both on the pull request and on the trunk |
| Slug | `dietary-filter` |
| Source locator convention | note identifiers for `interview.md`; line ranges for the brief — both in `runs/20261020_0930/` |

**Sources this document is written from**, ranked before reading, per `CLAUDE.md` §4:

| Source (the copy in this repository) | Copied from | Revision | Rank | What it contributed |
|---|---|---|---|---|
| `docs/requirements/dietary-filter/runs/20261020_0930/interview.md` | written here — the interview `/feature` ran with the head of product | 2026-10-20 | 5 — wins a conflict with the brief | The owning role, the refusal shape (REQ-2), the multi-tag reading (A-2) and the blocking flag on CLAR-SHOP-diet-01 |
| `docs/requirements/dietary-filter/runs/20261020_0930/kitchen-brief.md` | the Larder product team's brief folder, page "Menu filters" | version 2, 2026-10-14 | 5 | Every requirement, the constraint, the exclusions and the open question |

Both rank 5. The interview sharpens the brief twice, at REQ-2 and at A-2, and no conflict arose.

## 2. Purpose and business outcome

Customer care answers about forty contacts a week from customers who cannot tell which of this
week's recipes suit their diet. They read every recipe's ingredients, and some give up and do not
order.

**The outcome this is judged by:** a vegetarian or vegan customer sees only the recipes of this
week's menu that suit them, in one step, and keeps that view when they reload or share the page.

## 3. Scope

**In scope** — each line citing the source that puts it in:

- Showing only the recipes of this week's menu that carry one diet tag — Derives from: `kitchen-brief.md` § What we need L23-25
- Refusing a diet the shop does not offer — Derives from: `kitchen-brief.md` § What we need L27-28; `interview.md` § note 3
- Keeping the chosen diet across a reload and a shared link — Derives from: `kitchen-brief.md` § What we need L30-31
- A gluten-free filter for certified recipes, held on its open question — Derives from: `kitchen-brief.md` § Gluten-free L38-40

**Out of scope** — each line with the reason and the role who owns the exclusion:

- Combining two diets in one filter — the brief excludes it in its own words; owner: head of product — Derives from: `kitchen-brief.md` § What we do not need L44
- Allergen information beyond the diet tags — separate work with Legal; owner: head of product — Derives from: `kitchen-brief.md` § What we do not need L46

## 4. Definitions

| Term | Definition as used here | Source |
|---|---|---|
| Diet tag | A word the kitchen attaches to a recipe, such as `vegetarian` or `vegan`. A recipe can carry several | `kitchen-brief.md` § What we need L24; `interview.md` § note 4 |
| Filtered menu | This week's menu with every recipe that does not carry the chosen diet tag hidden, in the kitchen's order | `kitchen-brief.md` § What we need L23-25, L33-34 |

## 5. Parties

| Role | Interest in this document | Decisions they own | Source |
|---|---|---|---|
| Head of product | Owns the outcome and signs this document | Which diets are offered | `interview.md` § note 2 |
| Food safety lead | Certifies a recipe as gluten-free | Who certifies a recipe, and how the certification reaches the catalogue (CLAR-SHOP-diet-01) | `kitchen-brief.md` § Gluten-free L38-40, § Not yet agreed L54 |

## 6. Requirements

### REQ-1 — A customer can show only the recipes that suit one diet

Derives from: `kitchen-brief.md` § What we need L23-25, L33-34

A customer chooses one diet, vegetarian or vegan, and sees only the recipes of this week's menu
that carry that diet's tag.

| ID | Criterion | Type | Source |
|---|---|---|---|
| REQ-1.AC-1 | With vegetarian chosen, every recipe shown carries the vegetarian tag, and every recipe of the menu that carries it is shown | positive | `kitchen-brief.md` § What we need L23-24; `interview.md` § note 4 |
| REQ-1.AC-2 | With vegan chosen, every recipe shown carries the vegan tag, and every recipe of the menu that carries it is shown | positive | `kitchen-brief.md` § What we need L23-24 |
| REQ-1.AC-3 | With no diet chosen, the full menu is shown, unchanged; going back to it from a filtered menu is one step | positive | `kitchen-brief.md` § What we need L25 |
| REQ-1.AC-4 | A filtered menu keeps the kitchen's order of the recipes it shows | positive | `kitchen-brief.md` § What we need L33-34 |
| REQ-1.AC-5 | A filtered menu shows each recipe with the same price and content as the full menu | negative | `kitchen-brief.md` § Constraints L50 |

### REQ-2 — A diet the shop does not offer is refused, never ignored

Derives from: `kitchen-brief.md` § What we need L27-28

A request for a diet the shop does not offer answers with a refusal and shows no recipes, so that a
full menu never looks filtered. The refusal follows the estate's error rules: std-http-apis.05
answers 400 for a parameter that fails validation, and std-http-apis.04 fixes the error body.

| ID | Criterion | Type | Source |
|---|---|---|---|
| REQ-2.AC-1 | A request for a diet the shop does not offer is refused with a message that says the diet is not offered, and shows no recipes | negative | `kitchen-brief.md` § What we need L27-28; `interview.md` § note 3 |
| REQ-2.AC-2 | The refusal does not repeat the value the customer sent | negative | `interview.md` § note 3 |

### REQ-3 — The chosen diet survives a reload and a shared link

Derives from: `kitchen-brief.md` § What we need L30-31

| ID | Criterion | Type | Source |
|---|---|---|---|
| REQ-3.AC-1 | The chosen diet is part of the page's address | positive | `kitchen-brief.md` § What we need L30-31 |
| REQ-3.AC-2 | Opening that address in a new browser shows the same filtered menu | positive | `kitchen-brief.md` § What we need L30-31 |

### REQ-4 — A customer can show only the recipes certified gluten-free

Derives from: `kitchen-brief.md` § Gluten-free L38-40

**Held on the blocking CLAR-SHOP-diet-01; `/decompose` records it as `Unresolved`, no key.**

| ID | Criterion | Type | Source |
|---|---|---|---|
| REQ-4.AC-1 | With gluten-free chosen, only recipes certified gluten-free are shown | positive | `kitchen-brief.md` § Gluten-free L38-40 |
| REQ-4.AC-2 | A recipe that is not certified is never shown under gluten-free, whatever its ingredients | negative | `kitchen-brief.md` § Gluten-free L38-40 |

## 7. Constraints

| Constraint | Type | Source | Consequence if it does not hold |
|---|---|---|---|
| The filter changes no price and no recipe content | business | `kitchen-brief.md` § Constraints L50 | A customer sees a price in the filtered menu that the order does not charge |

## 8. Coverage map

| Source part | Locator | Requirements | Disposition | Reason and owner |
|---|---|---|---|---|
| Context header and copy note | L1-13 | deliberately none | Out of scope | Metadata added when the brief was copied in; recorded in §1; requirements author |
| Why we are asking | L15-19 | deliberately none | Represented | Carried into §2 as the situation |
| What we need — one diet | L23-25 | REQ-1 | Represented | Fully carried |
| What we need — an unknown diet | L27-28 | REQ-2 | Represented | Fully carried, with the refusal shape from the interview |
| What we need — reload and share | L30-31 | REQ-3 | Represented | Fully carried |
| What we need — the kitchen's order | L33-34 | REQ-1 | Represented | REQ-1.AC-4 |
| Gluten-free | L36-40 | REQ-4 | Unresolved | UNRESOLVED — who certifies a recipe as gluten-free, and how the certification reaches the catalogue. Owner: food safety lead. Resolves: CLAR-SHOP-diet-01 closes. |
| What we do not need | L42-46 | deliberately none | Out of scope | Excluded by the source in its own words; head of product |
| Constraints | L48-50 | REQ-1 | Represented | REQ-1.AC-5 and the §7 row |
| Not yet agreed | L52-54 | REQ-4 | Unresolved | UNRESOLVED — who certifies a recipe as gluten-free, and how the certification reaches the catalogue. Owner: food safety lead. Resolves: CLAR-SHOP-diet-01 closes. |
| Interview notes 1-6 | `interview.md` § note 1-6 | REQ-1, REQ-2, REQ-4 | Represented | Notes 1, 2 and 6 confirm the reading, the role and the exclusion; note 3 is REQ-2; note 4 is A-2; note 5 is the hold on REQ-4 |

## 9. Clarifications

| ID | Question | Source | Blocking | Routed to | Status | Resolution | Resolved |
|---|---|---|---|---|---|---|---|
| CLAR-SHOP-diet-01 | Who certifies a recipe as gluten-free, and how does the certification reach the catalogue? | `kitchen-brief.md` § Gluten-free L38-40, § Not yet agreed L54; `interview.md` § note 5 | yes | Food safety lead | Open |  |  |

## 10. Assumptions and decisions

| # | Interpretation | Why it is defensible | Confidence | Source |
|---|---|---|---|---|
| A-1 | "This week's menu" is the menu of the current ISO week, as the shop shows it today | The brief speaks of the menu a customer sees; the shop already opens on the current week | derived | `kitchen-brief.md` § What we need L23 |
| A-2 | A recipe shows under every diet it is tagged with, so a vegan recipe tagged vegetarian too shows under vegetarian | The head of product chose it in the interview | stated | `interview.md` § note 4 |

Context: std-http-apis@a50f7b53a8e0:docs/standards/std-http-apis.md
Hub commit: de02dec97968a7b0f36447a8dff54cae73314f30
