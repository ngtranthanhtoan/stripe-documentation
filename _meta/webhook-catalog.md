# Webhook event catalog

Every event Stripe emits, grouped by source object. Names match `event.type` values you'll see in your webhook handler. Reflects API version `2026-04-22.dahlia`.

## Charge

- `charge.succeeded` — funds captured (or auth-only succeeded with `captured: false`).
- `charge.failed` — declined or errored.
- `charge.captured` — uncaptured charge later captured.
- `charge.refunded` — at least one refund attached. Fires *every* time a partial refund is added.
- `charge.updated` — most other field changes (description, metadata).
- `charge.expired` — uncaptured authorization expired without capture.
- `charge.pending` — async payment method (e.g. ACH) still settling.
- `charge.dispute.created` — chargeback opened. *This is the one you must page on.*
- `charge.dispute.updated` — evidence change.
- `charge.dispute.closed` — won, lost, or warning closed.
- `charge.dispute.funds_withdrawn` / `charge.dispute.funds_reinstated` — ledger movements.

## PaymentIntent

- `payment_intent.created`
- `payment_intent.processing`
- `payment_intent.requires_action` — 3DS / SCA / OXXO voucher / etc. needed.
- `payment_intent.succeeded` — terminal success. **Use this, not `charge.succeeded`, for modern flows.**
- `payment_intent.payment_failed` — terminal failure (or retryable depending on `last_payment_error.code`).
- `payment_intent.canceled`
- `payment_intent.amount_capturable_updated`
- `payment_intent.partially_funded` — multibanco / customer balance partial.

## SetupIntent

- `setup_intent.created`
- `setup_intent.succeeded` — instrument saved, can be reused.
- `setup_intent.setup_failed`
- `setup_intent.requires_action`
- `setup_intent.canceled`

## Refund

- `refund.created`
- `refund.updated`
- `refund.failed` — async refund (ACH, etc.) bounced.

## Payout

- `payout.created`
- `payout.paid` — money landed in your bank.
- `payout.failed` — bank rejected.
- `payout.canceled`
- `payout.updated`
- `payout.reconciliation_completed` — all balance transactions assigned to this payout.

## BalanceTransaction

No events — `balance.available` fires when funds roll from `pending` to `available`.

## Customer

- `customer.created` / `customer.updated` / `customer.deleted`
- `customer.source.*` — legacy card/bank source events.
- `customer.tax_id.*`
- `customer.discount.*`
- `customer.subscription.*` — see Subscription below.

## PaymentMethod

- `payment_method.attached` — attached to a customer.
- `payment_method.detached`
- `payment_method.updated`
- `payment_method.automatically_updated` — Stripe's card-account-updater service refreshed expiry/PAN.

## Mandate

- `mandate.updated` — customer revoked or status changed.

## Invoice

- `invoice.created` — draft created (auto from subscription or manual).
- `invoice.updated` — line/field change while still mutable.
- `invoice.deleted` — only fires for drafts.
- `invoice.finalized` — moved from draft to open.
- `invoice.finalization_failed` — auto-finalization couldn't complete.
- `invoice.paid` — terminal success.
- `invoice.payment_succeeded` — payment attempt succeeded (can fire multiple times if retried).
- `invoice.payment_failed` — payment attempt failed; dunning may retry.
- `invoice.payment_action_required` — 3DS or similar.
- `invoice.marked_uncollectible`
- `invoice.voided`
- `invoice.sent` — emailed to customer.
- `invoice.upcoming` — preview event N days before next invoice; useful for dynamic line additions.
- `invoice.will_be_due` — N days before due date (configurable).
- `invoice.overdue`

## InvoiceItem

- `invoiceitem.created`
- `invoiceitem.deleted`

## CreditNote

- `credit_note.created`
- `credit_note.updated`
- `credit_note.voided`

## Subscription

- `customer.subscription.created`
- `customer.subscription.updated` — almost every change, including status transitions.
- `customer.subscription.deleted` — actually means *canceled* (terminal).
- `customer.subscription.trial_will_end` — fires 3 days before trial ends.
- `customer.subscription.paused` / `customer.subscription.resumed`
- `customer.subscription.pending_update_applied` / `pending_update_expired`

## Subscription Schedule

- `subscription_schedule.created`
- `subscription_schedule.updated`
- `subscription_schedule.released`
- `subscription_schedule.canceled`
- `subscription_schedule.completed`
- `subscription_schedule.expiring`
- `subscription_schedule.aborted`

## Quote

- `quote.created`
- `quote.finalized`
- `quote.accepted`
- `quote.canceled`
- `quote.will_expire`

## Checkout Session

- `checkout.session.completed` — *this is the success event for hosted checkout*.
- `checkout.session.async_payment_succeeded`
- `checkout.session.async_payment_failed`
- `checkout.session.expired`

## Payment Link

- `payment_link.created`
- `payment_link.updated`

## Issuing

- `issuing_authorization.request` — synchronous webhook; you must reply within 2s to approve/decline.
- `issuing_authorization.created` / `updated`
- `issuing_card.created` / `updated`
- `issuing_cardholder.created` / `updated`
- `issuing_dispute.created` / `updated` / `closed` / `funds_reinstated` / `funds_rescinded`
- `issuing_transaction.created` / `updated`
- `issuing_personalization_design.activated` / `deactivated` / `rejected` / `updated`
- `issuing_token.created` / `updated`

## Treasury

- `treasury.financial_account.created` / `features_status_updated`
- `treasury.transaction.created`
- `treasury.outbound_transfer.*` (created, posted, returned, canceled, expected_arrival_date_updated, tracking_details_updated)
- `treasury.outbound_payment.*`
- `treasury.inbound_transfer.*`
- `treasury.received_credit.created` / `failed` / `succeeded`
- `treasury.received_debit.created`
- `treasury.credit_reversal.*`
- `treasury.debit_reversal.*`

## Connect

- `account.updated` — *the* event for capability/requirement changes on a connected account.
- `account.application.authorized` / `deauthorized`
- `account.external_account.created` / `updated` / `deleted`
- `capability.updated`
- `person.created` / `updated` / `deleted`
- `application_fee.created` / `refunded`
- `application_fee.refund.updated`
- `transfer.created` / `updated` / `reversed`
- `topup.created` / `succeeded` / `failed` / `canceled` / `reversed`

## Radar

- `radar.early_fraud_warning.created` / `updated`
- `review.opened` / `closed`

## Identity

- `identity.verification_session.created` / `processing` / `verified` / `requires_input` / `canceled` / `redacted`

## Tax

- `tax.settings.updated`

## Financial Connections

- `financial_connections.account.created` / `updated` / `refreshed_balance` / `refreshed_transactions` / `refreshed_ownership` / `deactivated` / `disconnected` / `reactivated`

## Climate

- `climate.order.canceled` / `delayed` / `product_substituted` / `confirmed` / `delivered`
- `climate.product.created` / `pricing_updated`

## Billing meters / credits

- `billing.meter.created` / `updated` / `deactivated` / `reactivated`
- `billing.alert.triggered`
- `billing.credit_grant.created` / `updated`

## Reporting & Sigma

- `reporting.report_run.succeeded` / `failed`
- `sigma.scheduled_query_run.created`

## Source / Order (legacy)

- `source.*` — legacy Sources flow, do not use for new integrations.
- `order.*` — old Orders API (separate from new orders, deprecated).

---

## How to subscribe to a subset

When creating a [WebhookEndpoint](../19-webhooks/webhook-endpoints.md), pass `enabled_events: ['payment_intent.succeeded', …]` or `enabled_events: ['*']` for everything. Subscribing to `*` is fine in development; in production, list explicitly so a future Stripe release adding a new event doesn't blast your handler with unexpected types.
