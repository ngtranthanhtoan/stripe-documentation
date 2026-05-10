# `_meta/` — cross-cutting reference

These files don't document a specific Stripe API resource. They document the *project itself* (template, progress) and aspects of Stripe that span every category (the money model, the state machines, the webhook events, the glossary, the API version pin).

| File | What it is |
|---|---|
| [api-version.md](api-version.md) | Which Stripe API version this project documents and how to upgrade. |
| [glossary.md](glossary.md) | Cross-cutting Stripe terms (idempotency key, expansion, livemode, application_fee_amount, …). |
| [money-flow.md](money-flow.md) | How a dollar moves through Stripe end-to-end, in one diagram. |
| [state-machines.md](state-machines.md) | Every state machine in the project, in one place. |
| [webhook-catalog.md](webhook-catalog.md) | Every webhook event grouped by source object. |
| [template.md](template.md) | The 12-section structure every object guide follows. Copy in when adding a new resource. |
| [progress.md](progress.md) | Per-object status (deep / stub / N/A) and inventory. |

Object guides cross-reference these via relative links like `[Customer](../01-core-resources/customers.md)` or `[idempotency key](../_meta/glossary.md#idempotency-key)`.
