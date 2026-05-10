# 02 — Payment methods

The instruments customers pay you with — cards, bank accounts, wallets, BNPL, redirect-based methods. The modern object is [PaymentMethod](payment-methods.md); everything else here is either a configuration container or a legacy form.

| Object | One-liner |
|---|---|
| [PaymentMethod](payment-methods.md) | Reusable instrument representation (card, bank, BNPL, wallet). The modern object you'll work with daily. |
| [Payment Method Configuration](payment-method-configurations.md) | A Dashboard-managed bundle of PM types you offer at checkout. Referenced by PaymentIntent / Checkout Session. |
| [Payment Method Domain](payment-method-domains.md) | Domain registered with Stripe so Apple Pay / Google Pay / Link can render on it. |
| [Bank Account](bank-accounts.md) | Legacy bank-account representation (sub-resource of Customer/Account). Largely supplanted by PaymentMethod and ExternalAccount. |
| [Card](cards.md) | Legacy card representation (sub-resource of Customer/Account). Largely supplanted by PaymentMethod. |
| [Source](sources.md) | Legacy multi-step payment instrument. **Deprecated** — do not build on it for new integrations. |

## Card vs. PaymentMethod (why both exist)

`Card` predates `PaymentMethod`. In old Stripe, you'd `POST /v1/customers/:id/sources` with a `tok_visa` and get a Card back. That model couldn't represent non-card PMs cleanly, didn't support 3DS-ready flows, and forced PCI exposure into the integration.

`PaymentMethod` (introduced 2019, dominant since ~2020) unifies everything: cards, ACH, SEPA, BACS, OXXO, Klarna, AfterPay, AliPay, WeChat, Pix, Link, Apple/Google Pay tokens — all expose a single resource shape with a `type` discriminator.

For new code, ignore `Card` and `Source` entirely. Read `PaymentMethod`.
