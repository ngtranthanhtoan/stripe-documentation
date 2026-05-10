# 12 — Identity

Stripe Identity verifies a user's government ID + selfie + (optionally) data accuracy. Used for KYC, age gating, marketplace seller verification, sensitive-action confirmation.

| Object | One-liner |
|---|---|
| [Verification Session](verification-sessions.md) | One verification flow for one user. State machine: `requires_input → processing → verified | requires_input | canceled`. |
| [Verification Report](verification-reports.md) | Immutable report of one *attempt* within a session. Sessions can have multiple reports if user retries. |

## Session vs. Report

The **Session** is the user-facing handle ("verify Jane"); it can span multiple attempts. The **Report** is a single attempt (one ID upload + one selfie + checks). When a session ends `verified`, you read the latest Report for the actual extracted data and check results.

Reports can be **redacted** for compliance — after redaction the PII fields are wiped but the result enums remain.
