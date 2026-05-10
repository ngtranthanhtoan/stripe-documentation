# 20 — Apps

Resources used by Stripe Apps — third-party (or first-party) apps installed on a Stripe account that extend the Dashboard with custom UI, automation, and integrations.

| Object | One-liner |
|---|---|
| [Secret](secrets.md) | Encrypted key/value storage scoped to your installed App + (optionally) a specific user within it. App-private storage Stripe manages for you. |

If you're building a Stripe App, this is one of the few server-side state primitives Stripe offers — useful for storing OAuth tokens, per-merchant config, or anything you don't want to host yourself.
