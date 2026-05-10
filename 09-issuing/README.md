# 09 — Issuing

Stripe Issuing lets you *create cards* that *you* issue (virtual or physical), to your employees, contractors, or customers. The flow is the inverse of payments: instead of receiving money via cards, you issue cards that spend.

| Object | One-liner |
|---|---|
| [Authorization](authorizations.md) | A card-network request to spend on a card you issued. You can approve/decline synchronously via webhook. |
| [Cardholder](cardholders.md) | The person or business holding the card. KYC'd. |
| [Card](cards.md) | One issued card (virtual or physical). |
| [Dispute](disputes.md) | A dispute *you* file (as the issuer) against a transaction the cardholder claims was wrong. |
| [Funding Instructions](funding-instructions.md) | Where to wire money to fund the Issuing balance. |
| [Personalization Design](personalization-designs.md) | Visual design template for physical cards. |
| [Physical Bundle](physical-bundles.md) | A bundle of card stock + carrier + envelope used for physical card production. |
| [Token](tokens.md) | A network token (Apple Pay, Google Pay) provisioned for an issued card. |
| [Transaction](transactions.md) | The settled record of a completed Authorization. |
| [Settlement](settlements.md) | A daily aggregate of network settlement activity. |
| [Dispute Settlement Detail](dispute-settlement-details.md) | Per-dispute settlement breakdown. |

## Authorization is synchronous

Unlike most webhooks, `issuing_authorization.request` is a *synchronous* event: Stripe holds the card-network request open while it waits for your `200 OK` reply. You have **2 seconds** to approve or decline. Miss the window and Stripe falls back to your default rule (typically allow, configurable). Your handler must be fast and reliable.

## Issuing has its own balance

The Issuing balance is separate from your Payments balance. To pay for transactions, you fund Issuing from your bank (via [Funding Instructions](funding-instructions.md)) or transfer from your Payments balance. Cards spend from this Issuing balance.
