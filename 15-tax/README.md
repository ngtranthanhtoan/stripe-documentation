# 15 — Tax

Stripe Tax computes the right tax rate for every transaction (US sales tax, EU VAT, GST, etc.) and tracks where you're registered. Replaces the older manual `tax_rate` model for most users.

| Object | One-liner |
|---|---|
| [Calculation](calculations.md) | A standalone tax computation for a basket of line items + a customer location. Used outside of Invoices/Checkout. |
| [Transaction](transactions.md) | A finalized tax record (created on payment of an invoice with `automatic_tax`). Source of truth for tax filings. |
| [Registration](registrations.md) | Your tax registration in a jurisdiction (state, country). Stripe only collects tax where you're registered. |
| [Settings](settings.md) | Account-wide Tax config: default tax behavior, head office, tax IDs you collect. |
| [Association](associations.md) | Links a Tax Calculation to the resulting payment, used for reconciliation. |

## Calculation vs. Transaction

A **Calculation** is computed but not yet binding — used at quote time or during a custom checkout flow. A **Transaction** is a finalized commit: it's what shows up on your tax filings and what you owe authorities.

For Invoice / Checkout flows with `automatic_tax.enabled=true`, Stripe creates and commits the Transaction for you when payment succeeds.
