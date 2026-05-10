# 24 — Profiles

New in API version `2026-04-22.dahlia`. A unified per-end-user profile that spans Stripe products. Lets you reference the same person across Payments, Identity, Issuing, Treasury without duplicating identity records or re-doing KYC.

| Object | One-liner |
|---|---|
| [Profile](profiles.md) | A persistent identity record for an end user. Pluggable into Customer, Cardholder, Verification Session, Treasury Financial Account holder. |

## Status

Brand new. Stripe documentation is still being filled out for this API. Expect the Profile model to evolve significantly across the next few `dahlia.X` releases. Pin your code to a specific Stripe-Version and re-read the changelog before upgrading.
