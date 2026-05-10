# 11 — Treasury

Banking-as-a-service. With Treasury, your platform offers its connected accounts a Stripe-issued bank account: receive ACH, hold balance, send wires, get statements. Adjacent to (but distinct from) the Payments balance.

| Object | One-liner |
|---|---|
| [Financial Account](financial-accounts.md) | The Stripe-issued bank account itself. Has routing/account numbers, balance, allowed features. |
| [Financial Account Features](financial-account-features.md) | Per-feature enablement state for a Financial Account (ACH, wires, debit cards, …). |
| [Transaction](transactions.md) | A complete money movement on the FA's ledger (one entry per Transaction Entry pair). |
| [Transaction Entry](transaction-entries.md) | A single side of a money movement (the leg of a journal entry). |
| [Outbound Transfer](outbound-transfers.md) | Send money from the FA to an external bank (your platform-controlled action). |
| [Outbound Payment](outbound-payments.md) | Send money from the FA to an external bank (the connected account's action — has identity verification). |
| [Inbound Transfer](inbound-transfers.md) | Pull money from a connected external bank into the FA. |
| [Received Credit](received-credits.md) | Money arrived at the FA from outside (ACH credit, wire, etc.). |
| [Received Debit](received-debits.md) | Money was pulled from the FA from outside (ACH debit). |
| [Credit Reversal](credit-reversals.md) | A previously-received credit was reversed by the originator. |
| [Debit Reversal](debit-reversals.md) | A previously-received debit was reversed. |

## Treasury is geographically restricted

Treasury is **US-only** (as of `2026-04-22.dahlia`). Connected accounts must be in the US, and the Treasury features come from Stripe's bank partners (e.g. Evolve Bank & Trust). Eligibility, KYC, and compliance bars are higher than for Payments.

## Two ledgers, two truths

A connected account that uses both Payments and Treasury has *two* balances:

- **Payments balance** — funds from Charges, before Payout.
- **Treasury balance** — funds in the Financial Account.

You can move money between them via Outbound Transfers (Treasury) and Top-ups (the Connect side). They are not the same balance.
