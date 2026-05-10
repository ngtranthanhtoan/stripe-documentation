# 23 — Agentic commerce

New in API version `2026-04-22.dahlia`. Resources for AI-agent-initiated payments: when an autonomous agent (operated by your customer) takes a payment action on their behalf, this layer carries the consent, the per-transaction caps, and the agent identity.

| Object | One-liner |
|---|---|
| [Token](tokens.md) | A consent token issued by a customer to an agent, scoping what payments the agent may make on their behalf (amount caps, merchant whitelists, time bounds). |

## Why this exists

LLM agents can already book travel, order groceries, refill subscriptions. Without an agentic-commerce primitive, every merchant has to bolt on its own consent + cap mechanism. This API standardizes:

- Customer issues consent → token records limits.
- Agent presents token at payment time → Stripe enforces caps.
- Customer can revoke at any time → token invalidated.

Expect this category to grow rapidly in subsequent API versions.
