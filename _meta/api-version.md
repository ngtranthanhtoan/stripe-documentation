# API version pinning

This project documents Stripe API version **`2026-04-22.dahlia`** (latest stable as of 2026-05-06).

## How to interpret a Stripe version

Stripe versions look like `YYYY-MM-DD.codename` (e.g. `2026-04-22.dahlia`). They are **frozen forever**: an account pinned to `2024-06-20` keeps receiving the response shape and webhook payloads from that release date, even years later. Stripe layers behavior changes on top of API versions — newer integrations opt-in via a `Stripe-Version` request header or by upgrading on the Dashboard.

There are two version channels:

- **Account default version** — set on the Dashboard. Used when no header is sent. Webhooks use this version unless the `WebhookEndpoint` was created with an explicit `api_version`.
- **Per-request `Stripe-Version` header** — overrides the account default for that one call.

> **Pitfall.** Webhook payloads use the version the *endpoint* was created with, not the account default. If you upgrade your account but never recreate the webhook, you keep getting old-shape events.

## Why pin a project to one version

Field names, enum values, and even resource shapes change between versions. For learning material to stay coherent, it must point at one version. This project assumes `2026-04-22.dahlia` everywhere unless a doc explicitly says otherwise.

## Notable changes that shape this project

The `dahlia` release added or expanded:

- **Agentic commerce tokens** — new resource family for AI-agent-initiated payments. See [23-agentic-commerce/](../23-agentic-commerce/README.md).
- **Stripe Profiles API** — new resource family for cross-product customer identity. See [24-profiles/](../24-profiles/README.md).
- **Sunbit BNPL** and **Pix recurring** — new payment methods listed under [02-payment-methods/payment-methods/](../02-payment-methods/payment-methods.md).
- **Blik recurring** — Blik became a recurring-capable payment method.
- **Global Payouts to Japan and China** — new cross-border destinations for [Payout](../01-core-resources/payouts.md).
- **Programmatic Workflow invocation** — Workflows are no longer Dashboard-only.
- **Tax registration types** for ticket-sales jurisdictions.

## Updating this project to a future version

When Stripe releases a newer version:

1. Read the [official changelog](https://docs.stripe.com/changelog) end-to-end.
2. Update the version string in this file and at the top of every resource README that references a changed field.
3. Add a `## Changes from <prev>.codename` section to any object whose shape moved.
4. Bump [_meta/webhook-catalog.md](webhook-catalog.md) for new/renamed events.
