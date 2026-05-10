# 16 — Climate

Stripe Climate orders carbon removal on your behalf. Either fixed-amount orders or % of revenue. The Climate API exposes the order lifecycle and the supplier portfolio.

| Object | One-liner |
|---|---|
| [Order](orders.md) | A purchase of carbon removal tonnage. State machine: `awaiting_funds → confirmed → delivered`. |
| [Product](products.md) | A carbon-removal product offered by a supplier (e.g. mineralization, ocean alkalinity). |
| [Supplier](suppliers.md) | A vendor in Stripe Climate's portfolio (Charm Industrial, Heirloom, etc.). |

This category is intentionally narrow — Stripe Climate is a small, opinionated API. Most teams set up a fixed monthly order and never touch it again.
