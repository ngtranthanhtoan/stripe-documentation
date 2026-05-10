# 13 — Reporting

Programmatic access to Stripe's pre-built financial reports — the same ones you can download from the Dashboard.

| Object | One-liner |
|---|---|
| [Report Type](report-types.md) | Catalog of available reports (`balance.summary.1`, `charges.1`, `payouts.1`, …). Read-only. |
| [Report Run](report-runs.md) | A request to generate one report for a given time window. Async — you poll until it completes, then download the file. |

## Reporting vs. Sigma vs. raw API

- **Reporting** — Stripe pre-defines the schema. Easy, no SQL.
- **Sigma** — you write SQL against a near-realtime warehouse of your account's data. Pay per query.
- **Raw API + your own ETL** — list resources, sync to your warehouse, derive whatever. Most control.

Most teams use Reporting for finance/accounting (accounts receivable, sales tax, monthly P&L) and Sigma or raw API for product analytics.
