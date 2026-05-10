# State machines, all in one place

Cross-reference for every state-bearing object in this project. Each diagram is the canonical lifecycle; follow the link for what each state allows.

## PaymentIntent

```mermaid
stateDiagram-v2
    [*] --> requires_payment_method
    requires_payment_method --> requires_confirmation: attach PM
    requires_confirmation --> requires_action: 3DS needed
    requires_action --> processing: customer auth'd
    requires_confirmation --> processing: no auth needed
    requires_payment_method --> processing: confirm with PM in one call
    processing --> succeeded
    processing --> requires_payment_method: PM declined, retryable
    processing --> canceled
    requires_payment_method --> canceled
    requires_confirmation --> canceled
    requires_action --> canceled
    succeeded --> [*]
    canceled --> [*]
```

Detail: [PaymentIntent](../01-core-resources/payment-intents.md).

## Charge

A Charge has no `status` enum but has booleans that act like one:

- `captured: false` + `status: succeeded` → authorization only (uncaptured).
- `captured: true` + `status: succeeded` → captured, funds settling.
- `status: failed` → declined or errored at the network.
- `refunded: true` (full) or partial via `amount_refunded` → reversed.
- `disputed: true` → customer filed chargeback.

Detail: [Charge](../01-core-resources/charges.md).

## Refund

```mermaid
stateDiagram-v2
    [*] --> pending
    pending --> succeeded
    pending --> failed
    pending --> canceled: ACH refund withdrawn
    pending --> requires_action: rare, e.g. card update needed
    requires_action --> succeeded
    requires_action --> failed
```

Detail: [Refund](../01-core-resources/refunds.md).

## Dispute

```mermaid
stateDiagram-v2
    [*] --> warning_needs_response: early warning
    [*] --> needs_response
    needs_response --> under_review: evidence submitted
    warning_needs_response --> warning_under_review
    warning_under_review --> warning_closed
    under_review --> won
    under_review --> lost
    needs_response --> lost: timed out
    won --> [*]
    lost --> [*]
    warning_closed --> [*]
```

Detail: [Dispute](../01-core-resources/disputes.md).

## Payout

```mermaid
stateDiagram-v2
    [*] --> pending
    pending --> in_transit: handed to bank
    in_transit --> paid
    in_transit --> failed
    pending --> canceled: you canceled
    paid --> [*]
    failed --> [*]
    canceled --> [*]
```

Detail: [Payout](../01-core-resources/payouts.md).

## Invoice

```mermaid
stateDiagram-v2
    [*] --> draft
    draft --> open: finalize
    draft --> deleted: only draft can be deleted
    open --> paid
    open --> uncollectible: you give up on collecting
    open --> void: you cancel an unpaid invoice
    uncollectible --> paid: marked paid out-of-band
    paid --> [*]
    void --> [*]
    deleted --> [*]
```

Once an invoice is `open`, **its lines are immutable** — no more InvoiceItems, no field edits except metadata, description, and a few payment-config fields. Reductions to a finalized invoice happen via [CreditNote](../06-billing/credit-notes.md).

Detail: [Invoice](../06-billing/invoices.md).

## Subscription

```mermaid
stateDiagram-v2
    [*] --> incomplete: first invoice unpaid
    [*] --> trialing: trial_period > 0
    [*] --> active: paid immediately
    incomplete --> active: payment succeeds within 23h
    incomplete --> incomplete_expired: not paid in 23h
    trialing --> active: trial ends
    trialing --> past_due: trial ends + payment fails
    active --> past_due: renewal payment fails
    past_due --> active: payment recovered
    past_due --> canceled: dunning gives up
    past_due --> unpaid: dunning gives up (alt)
    active --> canceled: cancel API
    canceled --> [*]
    incomplete_expired --> [*]
    unpaid --> [*]
```

Detail: [Subscription](../06-billing/subscriptions.md).

## SetupIntent

```mermaid
stateDiagram-v2
    [*] --> requires_payment_method
    requires_payment_method --> requires_confirmation
    requires_confirmation --> requires_action
    requires_action --> processing
    requires_confirmation --> processing
    processing --> succeeded
    processing --> requires_payment_method
    requires_payment_method --> canceled
    requires_confirmation --> canceled
    succeeded --> [*]
    canceled --> [*]
```

Detail: [SetupIntent](../01-core-resources/setup-intents.md).

## Checkout Session

```mermaid
stateDiagram-v2
    [*] --> open
    open --> complete: customer paid / confirmed
    open --> expired: 24h with no completion
    complete --> [*]
    expired --> [*]
```

Detail: [Checkout Session](../04-checkout/sessions.md).

## Issuing Authorization

```mermaid
stateDiagram-v2
    [*] --> pending
    pending --> closed: settled
    pending --> reversed: merchant reversed
    pending --> expired: never settled
```

Detail: [Issuing Authorization](../09-issuing/authorizations.md).

## Quote

```mermaid
stateDiagram-v2
    [*] --> draft
    draft --> open: finalize
    open --> accepted: customer accepts
    open --> canceled
    accepted --> [*]
    canceled --> [*]
```

Detail: [Quote](../06-billing/quotes.md).

## Subscription Schedule

```mermaid
stateDiagram-v2
    [*] --> not_started
    not_started --> active: start_date reached
    active --> completed: phases ended
    not_started --> canceled
    active --> canceled
    active --> released: detached from subscription
```

Detail: [SubscriptionSchedule](../06-billing/subscription-schedules.md).

## Verification Session (Identity)

```mermaid
stateDiagram-v2
    [*] --> requires_input
    requires_input --> processing
    processing --> verified
    processing --> requires_input: needs new doc
    requires_input --> canceled
    verified --> [*]
    canceled --> [*]
```

Detail: [Identity VerificationSession](../12-identity/verification-sessions.md).
