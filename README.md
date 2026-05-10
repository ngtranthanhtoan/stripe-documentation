# Learning Stripe — In and Out

A structured study project to learn the Stripe platform end-to-end, one resource at a time.

> **API version pinned:** `2026-04-22.dahlia` (latest as of 2026-05-06).
> See [_meta/api-version.md](_meta/api-version.md) for how this is kept current.

## How this project is organized

Stripe exposes ~150 API resources across ~25 product domains. Every resource gets its own folder under a numbered category, and every folder has one markdown guide (`README.md`) that follows the same template:

1. **What it is** — plain-English definition and place in the Stripe domain.
2. **Why it exists** — the business problem it solves.
3. **Lifecycle & states** — the full state machine, every transition, and what each state allows.
4. **Anatomy of the object** — the fields you must understand (not the full reference).
5. **Relationships** — parents, children, sibling references; mermaid diagrams where useful.
6. **Common workflows** — step-by-step recipes for the things you actually do.
7. **Webhook events** — what fires, when, and what listeners typically do.
8. **Idempotency, retries & race conditions** — what goes wrong on a double-call and what Stripe handles for you.
9. **Test-mode tips** — fixtures, magic tokens, test clocks.
10. **Connect considerations** — what changes on a connected account.
11. **Common pitfalls** — real mistakes engineers make.
12. **Further reading** — links into the official docs.

The template lives at [_meta/template.md](_meta/template.md). When stubbing a new object, copy that file in.

## Categories

| # | Category | Folder |
|---|---|---|
| 01 | Core resources (money movement primitives) | [01-core-resources/](01-core-resources/README.md) |
| 02 | Payment methods | [02-payment-methods/](02-payment-methods/README.md) |
| 03 | Products & catalog | [03-products/](03-products/README.md) |
| 04 | Checkout | [04-checkout/](04-checkout/README.md) |
| 05 | Payment Links | [05-payment-links/](05-payment-links/README.md) |
| 06 | Billing (invoices, subscriptions, metering, credits) | [06-billing/](06-billing/README.md) |
| 07 | Connect (multi-party platforms) | [07-connect/](07-connect/README.md) |
| 08 | Fraud & Radar | [08-fraud/](08-fraud/README.md) |
| 09 | Issuing (card issuing) | [09-issuing/](09-issuing/README.md) |
| 10 | Terminal (in-person payments) | [10-terminal/](10-terminal/README.md) |
| 11 | Treasury (banking-as-a-service) | [11-treasury/](11-treasury/README.md) |
| 12 | Identity (KYC) | [12-identity/](12-identity/README.md) |
| 13 | Reporting | [13-reporting/](13-reporting/README.md) |
| 14 | Sigma (scheduled queries) | [14-sigma/](14-sigma/README.md) |
| 15 | Tax | [15-tax/](15-tax/README.md) |
| 16 | Climate (carbon removal) | [16-climate/](16-climate/README.md) |
| 17 | Forwarding | [17-forwarding/](17-forwarding/README.md) |
| 18 | Entitlements | [18-entitlements/](18-entitlements/README.md) |
| 19 | Webhooks (the configuration object itself) | [19-webhooks/](19-webhooks/README.md) |
| 20 | Apps (Stripe Apps platform) | [20-apps/](20-apps/README.md) |
| 21 | Financial Connections | [21-financial-connections/](21-financial-connections/README.md) |
| 22 | Crypto (on-ramp) | [22-crypto/](22-crypto/README.md) |
| 23 | Agentic commerce (new in 2026) | [23-agentic-commerce/](23-agentic-commerce/README.md) |
| 24 | Profiles (new in 2026) | [24-profiles/](24-profiles/README.md) |

## Suggested learning path

Stripe is huge; don't read it linearly. Follow the dependency order:

1. **Money model first.** Read these in order: [Balance](01-core-resources/balance.md), [BalanceTransaction](01-core-resources/balance-transactions.md), [Charge](01-core-resources/charges.md), [Refund](01-core-resources/refunds.md), [Payout](01-core-resources/payouts.md), [Dispute](01-core-resources/disputes.md). Once you see how every cent ends up in `balance_transactions`, every later object will make sense.
2. **The modern payment flow.** [PaymentMethod](02-payment-methods/payment-methods.md) → [PaymentIntent](01-core-resources/payment-intents.md) → [SetupIntent](01-core-resources/setup-intents.md). This is what almost every integration uses today instead of raw Charges.
3. **Customers and saving instruments.** [Customer](01-core-resources/customers.md), [Mandate](01-core-resources/mandates.md), [Token](01-core-resources/tokens.md) (legacy), [ConfirmationToken](01-core-resources/confirmation-tokens.md).
4. **Catalog.** [Product](03-products/products.md), [Price](03-products/prices.md), [Coupon](03-products/coupons.md), [PromotionCode](03-products/promotion-codes.md), [Discount](03-products/discounts.md).
5. **Hosted UIs.** [Checkout Session](04-checkout/sessions.md), [Payment Link](05-payment-links/payment-links.md).
6. **Recurring billing.** [Invoice](06-billing/invoices.md), [InvoiceItem](06-billing/invoice-items.md), [Subscription](06-billing/subscriptions.md), [SubscriptionSchedule](06-billing/subscription-schedules.md), [CreditNote](06-billing/credit-notes.md), [Quote](06-billing/quotes.md).
7. **Webhooks & async truth.** [Event](01-core-resources/events.md), [WebhookEndpoint](19-webhooks/webhook-endpoints.md), [EventDestination](01-core-resources/event-destinations.md).
8. **Pick a vertical:** Connect, Issuing, Treasury, Terminal, Identity, Tax — only learn what your product needs.

## Cross-cutting reference

- [_meta/glossary.md](_meta/glossary.md) — terms that show up everywhere (idempotency key, expansion, livemode, application_fee_amount, …).
- [_meta/state-machines.md](_meta/state-machines.md) — every state machine in the project, in one place.
- [_meta/webhook-catalog.md](_meta/webhook-catalog.md) — every webhook event grouped by source object.
- [_meta/money-flow.md](_meta/money-flow.md) — how a dollar moves through Stripe end-to-end.

## Status

- [x] Folder structure for every resource
- [ ] Deep guides for the foundational objects (Customer, PaymentIntent, Charge, Invoice, Subscription, Account, …)
- [ ] Stubs for every remaining object using the template
- [ ] Cross-cutting reference docs in `_meta/`

Track progress in [_meta/progress.md](_meta/progress.md).
