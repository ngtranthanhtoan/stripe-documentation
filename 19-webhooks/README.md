# 19 — Webhooks

The configuration objects for Stripe → your-server event delivery. The events themselves are [Event](../01-core-resources/events.md); this category is the *subscription* mechanism.

| Object | One-liner |
|---|---|
| [Webhook Endpoint](webhook-endpoints.md) | A registered URL that receives event POSTs. Has its own signing secret and `enabled_events` whitelist. |

## WebhookEndpoint vs. EventDestination

Stripe is in the middle of replacing `webhook_endpoint` with the more general [EventDestination](../01-core-resources/event-destinations.md) (which can target Amazon EventBridge or a webhook). Both work as of `2026-04-22.dahlia`. New code can use either; existing webhook endpoints continue to function.

## Verify signatures

Every webhook POST includes a `Stripe-Signature` header. **Always** verify it before processing — without verification, anyone can POST fake events to your URL and trigger order fulfillment / refunds. Stripe SDKs include a `constructEvent(payload, signature, secret)` helper.
