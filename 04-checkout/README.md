# 04 — Checkout

Stripe-hosted (or embedded) payment pages. The fastest way to take payments — Stripe owns the UI, PCI scope, SCA, payment-method picker, localization, and updates.

| Object | One-liner |
|---|---|
| [Checkout Session](sessions.md) | One run of the Checkout flow. In `payment` / `subscription` / `setup` mode. Wraps a PaymentIntent or SetupIntent; for subscriptions, also creates the Subscription. |

## When to use Checkout

- You want a working payment page in an afternoon.
- You don't want to design the payment UI.
- You want Stripe to keep the PM picker, 3DS, and SCA logic up to date for you.
- You need basic order confirmation + a customizable success URL.

## When to NOT use Checkout

- You need the form embedded in a multi-step flow that *isn't* "go to a hosted URL."
- You need fine-grained control of the PM picker order or appearance.
- You're collecting payment as part of a complex multi-tenant UX.

For embedded use, prefer [Payment Element](https://docs.stripe.com/payments/payment-element) inside your own page. For hosted simplicity, use Checkout Session.

## Mode matters

A Checkout Session is one of three modes set at creation:

- **`payment`** — single Charge via a PaymentIntent under the hood.
- **`subscription`** — creates a Subscription (and its first Invoice + PI).
- **`setup`** — saves a PM via SetupIntent without charging.

The mode determines which line items and behaviors are valid.
