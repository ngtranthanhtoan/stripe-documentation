# 01 — Core resources

These are the primitives of "money moved." Almost every other resource in Stripe ultimately points at one of these. Read this category first.

| Object | One-liner |
|---|---|
| [Balance](balance.md) | Money sitting in your Stripe account, split into `pending` and `available` per currency. |
| [Balance Transaction](balance-transactions.md) | The ledger entry. Every cent that moves writes one. Source of truth for accounting. |
| [Charge](charges.md) | The record of a single attempted/completed payment. Carries the receipt, fees, and dispute pointer. |
| [Customer](customers.md) | Persistent record of someone you can charge again. Owns saved PMs, invoice defaults, balances. |
| [Customer Session](customer-sessions.md) | Short-lived client secret that lets Stripe Elements operate on a specific Customer. |
| [Dispute](disputes.md) | Chargeback the customer (or their bank) filed. State machine for evidence submission and resolution. |
| [Event](events.md) | Immutable record of "something happened in your account." Powers webhooks. |
| [Event Destination](event-destinations.md) | New-model webhook config (replaces the legacy `WebhookEndpoint`). |
| [File](files.md) | An uploaded file (dispute evidence, identity docs, branding assets). |
| [File Link](file-links.md) | A signed, time-bound URL to a `File`. |
| [Mandate](mandates.md) | Customer's recorded permission to debit their account (ACH, SEPA, BACS). Required for many recurring debits. |
| [PaymentIntent](payment-intents.md) | The orchestrator. Modern primitive that encapsulates 3DS/SCA, retries, async PMs. |
| [SetupIntent](setup-intents.md) | PaymentIntent's sibling for *saving* a PM without charging now. |
| [Setup Attempt](setup-attempts.md) | Per-attempt log entry inside a SetupIntent's lifetime. |
| [Payout](payouts.md) | Money leaving Stripe to land in your bank. |
| [Refund](refunds.md) | Reversal of a Charge. Has its own lifecycle and ledger entry. |
| [ConfirmationToken](confirmation-tokens.md) | Modern single-use credential created by Stripe.js to confirm a PI/SI server-side. |
| [Token](tokens.md) | Legacy single-use card/bank representation. Replaced by PaymentMethod for new code. |

## Reading order

If this is your first encounter with Stripe, take it in this sequence:

1. [Balance](balance.md) and [Balance Transaction](balance-transactions.md) — the model of money inside Stripe.
2. [Charge](charges.md) — the primitive event of "money came in."
3. [Refund](refunds.md) and [Dispute](disputes.md) — the things that take money back out.
4. [Payout](payouts.md) — how money exits Stripe to your bank.
5. [Customer](customers.md) — the persistent identity that ties payments together over time.
6. [PaymentMethod](../02-payment-methods/payment-methods.md) and [Mandate](mandates.md) — the instruments customers pay with.
7. [PaymentIntent](payment-intents.md) and [SetupIntent](setup-intents.md) — the orchestrators you'll actually code against.
8. [Event](events.md) and [Event Destination](event-destinations.md) — how you find out about state changes.
