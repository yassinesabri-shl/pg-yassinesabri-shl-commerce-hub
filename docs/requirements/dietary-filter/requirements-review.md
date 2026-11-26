## Review: dietary-filter — the requirements document against the menu filters brief

### VERDICT: APPROVED
Cycle: 1 of 2
Mode: feature-review
Reviewer: pm-critic
Document revision: 92c431ed762b6edd40ffbf9599ae1d3c1113033b

#### SUGGESTION
- [docs/requirements/dietary-filter/requirements.md:81] REQ-2 names the error rules of std-http-apis; when the storefront shows the refusal, say in the story which words the customer reads → carry the wording into the storefront's story as a criterion

### Acceptance-criterion coverage

| AC | Criterion (short) | Covered where | Covered |
|---|---|---|---|
| Context header and copy note L1-13 | metadata from the copy | §1 Document control, and an §8 row | YES |
| Why we are asking L15-19 | the situation | §2 Purpose | YES |
| What we need L23-34 | one diet, an unknown diet, reload and share, the kitchen's order | REQ-1, REQ-2, REQ-3 | YES |
| Gluten-free L36-40 | a filter for certified recipes | REQ-4, held on CLAR-SHOP-diet-01 | YES |
| What we do not need L42-46 | two diets at once; allergens | §3 Out of scope, with the owner | YES |
| Constraints L48-50 | no price or content change | §7, and REQ-1.AC-5 | YES |
| Not yet agreed L52-54 | who certifies gluten-free | §9 CLAR-SHOP-diet-01, blocking | YES |
| Interview notes 1-6 | reading, role, refusal, tags, hold, exclusion | §1; REQ-2; A-2; the hold on REQ-4 | YES |

Derived AC count: 8 · Derived covered: 8 · Author declared: 8 / 8 · Match: YES

### Citation spot-check

Sampled 8 of 26 citations (minimum 30%) · fabricated or drifted: 0 · NONE — note 4 says what A-2 says, and no more; REQ-4 uses the brief's own condition at L39, certification of the whole supply chain

<!--
  Written beside the document by /feature from the critic's returned text. The hash above is the
  document's bytes as reviewed.
-->
