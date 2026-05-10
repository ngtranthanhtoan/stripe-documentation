# 07 — Connect

Multi-party platforms: marketplaces, SaaS-with-payments, gig platforms, anything that takes payments *on behalf of* somebody else and routes money to them. Connect is its own ecosystem with parallel concepts (accounts, charges, transfers, fees) that overlay on the rest of Stripe.

| Object | One-liner |
|---|---|
| [Account](accounts.md) | A connected merchant. Carries identity (KYC), capabilities, bank routing, requirements. |
| [Account Link](account-links.md) | A short-lived URL the merchant visits to complete onboarding. |
| [Account Session](account-sessions.md) | Client secret powering Connect Embedded Components in your platform UI. |
| [Login Link](login-links.md) | A one-time URL into the Express Dashboard for a connected account. |
| [Application Fee](application-fees.md) | The cut your platform takes from a charge processed on a connected account. |
| [Application Fee Refund](application-fee-refunds.md) | Reverses an application fee — typically created when a charge is refunded. |
| [Capability](capabilities.md) | Per-product permission on a connected account (`card_payments`, `transfers`, `treasury`, …). |
| [Country Spec](country-specs.md) | What's required to onboard / what's supported in each country. Reference data. |
| [External Account](external-accounts.md) | A connected account's bank account or debit card used for payouts. |
| [Person](persons.md) | An owner / director / representative of a `company`-type Account. Required for KYC. |
| [Top-up](top-ups.md) | Funds you push *into* your platform's Stripe balance from your bank — used to fund transfers. |
| [Transfer](transfers.md) | Money movement from your platform balance to a connected account. |
| [Transfer Reversal](transfer-reversals.md) | Reverses a Transfer (full or partial). |

## Three ways to charge in Connect

You'll meet these constantly; pick one architecture per integration:

1. **Direct charge** — `Stripe-Account: acct_…` header. Charge lives on the connected account; platform takes `application_fee_amount`. Connected account owns disputes and PCI.
2. **Destination charge** — no header; `transfer_data.destination=acct_…` on the PI/Charge. Charge lives on the platform; Stripe automatically transfers net funds to the connected account.
3. **Separate charges and transfers** — Charge on the platform, Transfer to connected account created as a separate API call (often later). Maximum flexibility, maximum bookkeeping.

See each Charge type's pros/cons in [Charge](../01-core-resources/charges.md) → "Connect considerations."

## Three account types

- **Standard** — full Stripe account; merchant uses the standard Stripe Dashboard.
- **Express** — slimmed-down hosted onboarding + Express Dashboard.
- **Custom** — platform builds every UI; Stripe is API-only.

The right choice depends on how much UI control you want vs. how much you want Stripe to handle. See [Account](accounts.md) for the full breakdown.
