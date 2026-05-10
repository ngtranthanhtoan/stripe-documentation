# 03 — Products & catalog

How Stripe represents the *thing* you sell, the *price* you sell it at, and the discounts you apply. These are the building blocks of any catalog-driven flow (Checkout, Subscriptions, Invoices, Quotes).

| Object | One-liner |
|---|---|
| [Product](products.md) | The thing you sell. Has a name, description, images, optional features. **No price information lives here.** |
| [Price](prices.md) | The price for one Product, in one currency, with one billing cadence. Most Products have many Prices. |
| [Coupon](coupons.md) | A reusable discount template (% off, fixed amount, duration). Applied via Discount. |
| [Promotion Code](promotion-codes.md) | A customer-facing redemption code (e.g. `BLACKFRIDAY`) bound to a Coupon. |
| [Discount](discounts.md) | An *instance* of a coupon applied to a Customer / Subscription / Invoice. |
| [Tax Code](tax-codes.md) | Stripe's product taxonomy (`txcd_…`). Tells Stripe Tax how to tax this product per jurisdiction. |
| [Tax Rate](tax-rates.md) | Manually-defined tax rate (legacy/manual mode). Stripe Tax replaces these for most users. |
| [Shipping Rate](shipping-rates.md) | A reusable shipping option (price + display name) used in Checkout / Quotes / Invoices. |

## Product vs. Price (the most common confusion)

A `Product` is "what you sell" — a name, a description. A `Price` is "how much, how often, in what currency, under what billing model." The same Product can have many Prices: monthly+annual, USD+EUR+GBP, tiered+flat.

```
Product: "Acme Pro Plan"
├── Price: $10/mo USD
├── Price: $100/year USD
├── Price: €9/mo EUR
└── Price: $0.10 per API call (metered)
```

**Almost everything (Subscriptions, Checkout Sessions, Invoice line items) references Prices, not Products.** The Product is for display; the Price is the contract.
