# Stripe glossary

Terms that show up across many resources. If a guide uses one of these without defining it, look here.

### Account
The top-level container for everything you do with Stripe. Your Stripe account has its own settings, balance, API keys, and webhook endpoints. In Connect, an `Account` object represents a *connected* account (a merchant on your platform), not your platform.

### API key
The secret used to authenticate API requests. `sk_live_…` keys touch real money; `sk_test_…` keys touch test data. Restricted keys (`rk_…`) scope down to specific resources. Publishable keys (`pk_…`) are safe in browsers and can only create tokens / confirm intents.

### Application fee
The cut your Connect platform takes from a charge processed on a connected account. Set with `application_fee_amount` (direct charges) or `application_fee_amount` on a Transfer. Surfaces as an [ApplicationFee](../07-connect/application-fees.md) object.

### Authorization (cards)
The bank's "yes, the funds exist and I'm holding them" response. With Stripe, an authorization happens when a Charge is created with `capture: false`, or via Issuing when *you* are the issuer.

### Balance
Your money inside Stripe — not yet paid out to your bank. See [Balance](../01-core-resources/balance.md). Has `available` and `pending` buckets per currency.

### BalanceTransaction
The ledger entry. Every dollar movement (charge, refund, fee, payout, transfer, dispute hold) creates a `BalanceTransaction`. This is the source of truth for accounting. See [BalanceTransaction](../01-core-resources/balance-transactions.md).

### Capture
Telling the bank to actually move funds from a previously authorized hold. A captured Charge is on its way to your balance; an uncaptured one is just a hold.

### Connected account
A merchant account on your Connect platform. Identified by an `acct_…` ID. API calls on its behalf use the `Stripe-Account: acct_…` header.

### Customer
A persistent record of a person or business that pays you. Required for subscriptions, saved payment methods, and most invoices. See [Customer](../01-core-resources/customers.md).

### Destination charge
A charge created on the platform with `transfer_data[destination]` set, so funds and fees route to a connected account automatically. Contrast with *direct charge* and *separate charges and transfers*.

### Direct charge
A charge created directly on the connected account (`Stripe-Account` header). The connected account "owns" the charge; the platform takes a cut via `application_fee_amount`.

### Event
An immutable record of "something happened in your account." Drives webhooks. See [Event](../01-core-resources/events.md). All webhooks are events; not all events deliver as webhooks if no endpoint is subscribed.

### Expansion
The query parameter `expand[]=foo` that tells Stripe to inline a related object instead of returning just its ID. E.g. `expand[]=customer` on a Charge returns the full Customer in the response. Limited to 4 levels deep.

### Idempotency key
An arbitrary string you send in the `Idempotency-Key` header so Stripe deduplicates a request if you retry. Stored for 24 hours. Don't reuse across logically different requests — the second one returns the first one's response.

### Invoice
A statement of what a customer owes for one billing period. Can be one-off or driven by a subscription. See [Invoice](../06-billing/invoices.md).

### Livemode
Boolean field on every object that says whether it lives in live or test mode. Test-mode and live-mode objects never reference each other.

### Mandate
The customer's permission to debit them, usually for ACH/SEPA/BACS. Stripe stores a `Mandate` object as evidence. Required for many recurring debits. See [Mandate](../01-core-resources/mandates.md).

### Metadata
A key-value bag (40 keys, 500 chars each) you can attach to almost any object. Stripe ignores its contents — it's for *your* application's bookkeeping. Searchable in some queries.

### Payment Intent
The modern primitive for "I want to collect $X from this customer." Encapsulates 3DS, SCA, payment-method selection, retries. Replaces direct Charge creation for ~all new integrations. See [PaymentIntent](../01-core-resources/payment-intents.md).

### Payment Method
A reusable representation of an instrument (card, bank account, BNPL). Decoupled from Customer so you can confirm a payment without saving. See [PaymentMethod](../02-payment-methods/payment-methods.md).

### Payout
Funds leaving your Stripe balance to land in your external bank account. See [Payout](../01-core-resources/payouts.md). Default cadence is daily on a 2-day rolling basis (US).

### Refund
A reversal of all or part of a Charge. Creates its own object and ledger entry. See [Refund](../01-core-resources/refunds.md).

### SCA / 3DS
Strong Customer Authentication / 3-D Secure. EU regulation requiring step-up auth on many card payments. PaymentIntents handle this for you.

### Setup Intent
PaymentIntent's sibling for *saving* a payment method without charging right now. Used for trial subscriptions, deferred payments, on-file billing. See [SetupIntent](../01-core-resources/setup-intents.md).

### Stripe-Account header
HTTP header `Stripe-Account: acct_…` that makes a request act on behalf of a connected account. Required for direct charges and most Connect operations.

### Subscription
The recurring billing relationship between a Customer and one or more Prices. Drives Invoice creation on a schedule. See [Subscription](../06-billing/subscriptions.md).

### Test clock
A Stripe-managed virtual clock (`test_clock`) you can advance to fast-forward subscription renewals, trial endings, and invoice cycles in test mode. See [TestClock](../06-billing/test-clocks.md).

### Token
Legacy single-use representation of a card. Largely replaced by PaymentMethod. See [Token](../01-core-resources/tokens.md) and [ConfirmationToken](../01-core-resources/confirmation-tokens.md) (its modern successor).

### Transfer
Money movement between Stripe accounts (platform → connected account, or between two of your own balances). See [Transfer](../07-connect/transfers.md).

### Webhook
An HTTPS POST Stripe sends to your server when an Event occurs. Configured via [WebhookEndpoint](../19-webhooks/webhook-endpoints.md) and verified with `Stripe-Signature`.
