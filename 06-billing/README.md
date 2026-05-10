# 06 — Billing

The largest category. Recurring billing, one-off invoicing, metered usage, prepaid credits, customer-self-serve portal, quoting. If you sell subscriptions or send invoices, you live here.

| Object                                                                       | One-liner                                                                                                                                      |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| [Invoice](invoices.md)                                                       | Numbered, immutable-once-finalized statement of what a customer owes for one period.                                                           |
| [Invoice Item](invoice-items.md)                                             | A pending one-off line item that gets pulled into the next invoice for a Customer.                                                             |
| [Invoice Line Item](invoice-line-items.md)                                   | A line that *appears on* an invoice. Sourced from an InvoiceItem or a SubscriptionItem.                                                        |
| [Invoice Payment](invoice-payments.md)                                       | A payment attempt against an invoice (newer model exposing per-attempt detail).                                                                |
| [Invoice Rendering Template](invoice-rendering-templates.md)                 | Reusable PDF/page template a Customer or Invoice can point at for branded rendering.                                                           |
| [Credit Note](credit-notes.md)                                               | The legal way to reduce a finalized invoice (refund, balance credit, or out-of-band).                                                          |
| [Customer Balance Transaction](customer-balance-transactions.md)             | A debit/credit to the Customer's running balance. Auto-applied to next invoice.                                                                |
| [Customer Portal Session](customer-portal-sessions.md)                       | Short-lived URL to the Stripe-hosted self-service portal.                                                                                      |
| [Customer Portal Configuration](customer-portal-configurations.md)           | Defines what features (cancel, update PM, switch plan) the portal exposes.                                                                     |
| [Subscription](subscriptions.md)                                             | The recurring billing relationship. Generates invoices each cycle.                                                                             |
| [Subscription Item](subscription-items.md)                                   | One Price + quantity inside a Subscription.                                                                                                    |
| [Subscription Schedule](subscription-schedules.md)                           | Multi-phase script of what a Subscription should look like over time. Use for promo-then-full-price, scheduled upgrades, fixed-term contracts. |
| [Quote](quotes.md)                                                           | A draft proposal with line items + pricing that, when accepted, creates an Invoice or Subscription.                                            |
| [Billing Meter](billing-meters.md)                                           | Definition of a usage stream (e.g. `api_calls`, `gb_egress`).                                                                                  |
| [Billing Meter Event](billing-meter-events.md)                               | A single usage data point against a meter.                                                                                                     |
| [Billing Meter Event Adjustment](billing-meter-event-adjustments.md)         | A correction to previously-reported meter usage.                                                                                               |
| [Billing Meter Event Summary](billing-meter-event-summaries.md)              | Aggregated meter usage over a window.                                                                                                          |
| [Billing Credit Grant](billing-credit-grants.md)                             | Pre-paid credit you've granted a Customer (e.g. "$50 of API credit").                                                                          |
| [Billing Credit Balance Summary](billing-credit-balance-summary.md)          | Current credit balance per Customer/grant.                                                                                                     |
| [Billing Credit Balance Transaction](billing-credit-balance-transactions.md) | Per-event log of credit consumption.                                                                                                           |
| [Billing Alert](billing-alerts.md)                                           | Threshold-based alert ("notify me when usage hits 80% of plan").                                                                               |
| [Tax ID](tax-ids.md)                                                         | A Customer's tax registration number (VAT, GST, EIN, etc.).                                                                                    |
| [Test Clock](test-clocks.md)                                                 | Test-mode virtual clock you advance to fast-forward subscription cycles.                                                                       |
| [Plan (legacy)](plans-legacy.md)                                             | Old subscription pricing object. **Deprecated** — use Price.                                                                                   |
| [Usage Record (legacy)](usage-records-legacy.md)                             | Old metered-usage submission. **Deprecated** — use Billing Meter Events.                                                                       |

## Where to start

1. [Product](../03-products/products.md) and [Price](../03-products/prices.md) — the catalog.
2. [Customer](../01-core-resources/customers.md) — who you bill.
3. [Subscription](subscriptions.md) and [Invoice](invoices.md) — the recurring billing engine + its output.
4. [Credit Note](credit-notes.md) — how to make corrections after issuance.
5. [Subscription Schedule](subscription-schedules.md) — when one Subscription's lifecycle isn't enough.
6. [Billing Meter](billing-meters.md) family — for usage-based pricing.
7. [Quote](quotes.md) — for sales-led / B2B contracts.

## The deprecated layer

`Plan` and `UsageRecord` are pre-2018 objects kept for back-compat. Stripe still accepts them but the modern equivalents (Price, Billing Meter Events) are strictly better. Don't build new integrations on the legacy ones — folder is here for completeness.
