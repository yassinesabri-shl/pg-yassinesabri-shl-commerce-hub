---
name: estate-overview
description: What the Larder commerce estate is — the shop where a customer picks this week's recipes and places an order — for a reader who has never seen it.
globs: []
alwaysApply: false
kind: estate-overview
owner: lead architect
revision: 2026-10-20
origin: written by the lead architect from the repository list and the three READMEs, /add-context
---

# The Larder commerce estate: what it is

## 1. What the system does

Larder sells meal kits. Each week the kitchen publishes a menu of recipes. A customer opens the
shop, chooses recipes and portions, and places an order. The order enters through the
storefront, takes its prices from the catalogue, and ends up in pg-yassinesabri-shl-orders-api. From there the
operations estate picks, packs and dispatches it.

## 2. The parts

| Part (repository id) | What it is for | Who to ask |
|---|---|---|
| `pg-yassinesabri-shl-storefront-web` | The shop a customer uses: this week's menu, one recipe, the basket, the checkout and the order's status. | frontend lead |
| `pg-yassinesabri-shl-catalogue-api` | The recipes, their prices and the menu the kitchen publishes for each week. | backend lead |
| `pg-yassinesabri-shl-orders-api` | The record of every order, its frozen prices and its state. The operations hub governs it too. | backend lead |

## 3. Words the business uses

| Word | What it means here |
|---|---|
| recipe | One dish the kitchen can send, with its ingredients and its price for two portions. |
| menu | The recipes a customer can order for one ISO week, such as `2026-W43`. |
| published | A menu the kitchen has released. A published menu does not change. |
| basket | The recipes and quantities a customer has chosen and not yet ordered. |
| order | A basket the customer has placed, with the prices frozen at that moment. |
| minor unit | The smallest unit of a currency: pence for GBP, cents for EUR. |

## 4. Outside the estate

| System | What it does | Who owns it |
|---|---|---|
| The operations estate (`pg-yassinesabri-shl-operations-hub`) | Picks, packs and dispatches a paid order, and moves its state in pg-yassinesabri-shl-orders-api. | operations architect |
| The payment provider | Takes the customer's payment and tells Larder that an order is paid. | finance team |

UNRESOLVED — how a payment confirmation reaches pg-yassinesabri-shl-orders-api. Owner: lead architect. Resolves: the payment provider's integration review.
