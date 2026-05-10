# 05 — Payment Links

Persistent, shareable URLs that take payment. Like Checkout Sessions but reusable: one URL, many payments, no API call needed at point of sale.

| Object | One-liner |
|---|---|
| [Payment Link](payment-links.md) | A persistent URL that opens a Checkout Session for the configured Price(s). Created once, reused indefinitely. |

## When to use Payment Links

- "Send a payment URL in an email / SMS / chat."
- "Stick a buy button on a static landing page without writing backend code."
- "Sell a fixed-priced item from social media bios."

## How it relates to Checkout

A Payment Link is a *factory* for Checkout Sessions. Every visit to the URL creates a fresh Checkout Session. Lifecycle and webhooks of each visit are tracked on the Session, not the Link.

If you find yourself dynamically creating one Payment Link per customer, you're using the wrong tool — create Checkout Sessions instead.
