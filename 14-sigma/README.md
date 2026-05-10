# 14 — Sigma

Stripe's SQL-on-your-data product. Write a SQL query, schedule it, get results delivered to S3 / SFTP / email / webhook.

| Object | One-liner |
|---|---|
| [Scheduled Query](scheduled-queries.md) | A saved SQL query + cadence. Each run produces a downloadable result file and emits a webhook. |

## Mental model

Sigma exposes your Stripe data as Postgres-flavored tables (`charges`, `customers`, `subscriptions`, `balance_transactions`, …). Write a query once via the Dashboard or API, schedule it (hourly/daily/weekly), and Stripe runs it for you.

For one-off ad-hoc queries, use the Sigma Dashboard. For recurring runs that feed your data warehouse or email reports, use Scheduled Queries via API.
