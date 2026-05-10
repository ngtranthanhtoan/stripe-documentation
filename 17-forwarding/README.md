# 17 — Forwarding

Stripe Forwarding lets you send raw card data (PAN, CVC) to *non-Stripe* third parties without ever touching it yourself. Stripe acts as an in-line proxy: you POST a request body templated against a stored PaymentMethod, and Stripe injects the card details before forwarding.

| Object | One-liner |
|---|---|
| [Request](requests.md) | A single forwarded HTTP request. Stores the request, response, and template used. |

Used for: integrating with non-Stripe processors, network token provisioning, fraud-prevention vendors that need raw PAN. Niche, but the only way to keep PCI scope at SAQ-A while talking to providers that aren't Stripe-aware.
