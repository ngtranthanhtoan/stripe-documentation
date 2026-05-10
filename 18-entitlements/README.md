# 18 — Entitlements

A way to model "what features does this customer have access to?" decoupled from billing. Useful when "is the customer on the Pro plan?" is a question your code asks constantly.

| Object | One-liner |
|---|---|
| [Feature](features.md) | A named feature your product offers (`api_access`, `unlimited_seats`, `priority_support`). |
| [Product Feature](product-features.md) | Links a Feature to a Product, so customers on that Product get the feature. |
| [Active Entitlement](active-entitlements.md) | Read-only view: "what features does *this customer* currently have?" Computed from active Subscriptions + Product Features. |

## Why this exists

Without Entitlements, every product team builds an internal `is_pro_user(customer)` function that has to know about Subscription status, Plan IDs, trials, dunning grace periods, and overrides. Bugs creep in. Entitlements moves that lookup into Stripe: ask "what active entitlements does customer X have?" and Stripe returns the merged set across all their subscriptions, paused/active state, and trial flags.

Pair with a feature flag system in your code:

```python
if "api_access" in stripe.entitlements.active.list(customer=cus_id).data:
    serve_api_request()
```
