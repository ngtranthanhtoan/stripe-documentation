# 21 — Financial Connections

Plaid-equivalent product inside Stripe. Connect a customer's bank account, then read balances, ownership, and transactions, or instantly verify a US bank account for ACH debits.

| Object | One-liner |
|---|---|
| [Account](accounts.md) | A connected bank account at a financial institution. Carries balance/ownership/transaction permissions. |
| [Account Owner](account-owners.md) | Owner identity attached to a connected account (ownership-permission). |
| [Session](sessions.md) | A short-lived flow your customer goes through to authorize the connection. |
| [Transaction](transactions.md) | A single transaction read from the connected account (transactions-permission). |
| [Institution](institutions.md) | A financial institution Stripe supports for connection. |

## Why integrate

Two use cases:

1. **Instant US bank verification.** Lets you take ACH debit immediately without micro-deposit verification. Customer authorizes via Plaid-style flow → you get a verified `us_bank_account` PaymentMethod in seconds.
2. **Read bank data.** Underwriting, fraud, treasury management, accounting integrations.

Permissions (`balances`, `ownership`, `payment_method`, `transactions`) are granted per-Session and limit what your code can read.
