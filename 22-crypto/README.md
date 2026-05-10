# 22 — Crypto

Stripe's fiat-to-crypto on-ramp. The customer pays with card / bank, and Stripe (or a Stripe partner) delivers crypto to a wallet address you specify.

| Object | One-liner |
|---|---|
| [Onramp Session](onramp-sessions.md) | One on-ramp flow — destination wallet, network, asset, amount limits, customer KYC state. |

Stripe also supports stablecoin payments (USDC) and Crypto Pay payment-method types under [PaymentMethod](../02-payment-methods/payment-methods.md), but the on-ramp object is its own dedicated flow.
