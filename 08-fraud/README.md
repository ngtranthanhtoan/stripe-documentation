# 08 — Fraud & Radar

Stripe's anti-fraud layer. Radar is enabled by default; rules and reviews are opt-in upgrades. Disputes themselves live under [Core resources](../01-core-resources/disputes.md) — this category covers the *prevention* and *signal* side.

| Object | One-liner |
|---|---|
| [Early Fraud Warning](early-fraud-warnings.md) | Issuer warns Stripe a charge is likely to be disputed. **Pre-dispute signal**; refund proactively to avoid the chargeback. |
| [Review](reviews.md) | A charge Radar flagged for human inspection. Approved → charge stands; refused → refund + block. |
| [Radar Value List](radar-value-lists.md) | A named list of values (emails, IPs, BINs, …) referenced by Radar rules. |
| [Radar Value List Item](radar-value-list-items.md) | One entry in a value list. |

## Mental model

```
Charge attempted → Radar scores → outcome.risk_level
                              ↓
        elevated/highest → Radar rules fire (block / review / 3DS)
                              ↓
        Review created → human approves or refuses
                              ↓
        Days/weeks later → bank may issue Early Fraud Warning
                              ↓
        Days/weeks more → customer may file Dispute (chargeback)
```

The earlier in this chain you act, the cheaper. Refunding on EFW costs you the fee + the principal, but **avoids the chargeback fee and dispute-rate impact** that hurts your card-network reputation.
