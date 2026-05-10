# 10 — Terminal

In-person payments. Stripe Terminal is the SDK + reader hardware that lets you accept cards (chip, contactless, Tap to Pay) at a physical point of sale.

| Object | One-liner |
|---|---|
| [Connection Token](connection-tokens.md) | Short-lived token your client SDK uses to pair with a Reader. |
| [Location](locations.md) | A physical location (address). Readers are scoped to a Location. |
| [Reader](readers.md) | A registered card reader (BBPOS, Verifone, simulated, or Tap to Pay device). |
| [Hardware Order](hardware-orders.md) | An order you placed for physical readers from Stripe. |
| [Hardware Product](hardware-products.md) | Catalog entry for a piece of Terminal hardware. |
| [Hardware SKU](hardware-skus.md) | A specific orderable variant (color, region) of a hardware product. |
| [Hardware Shipping Method](hardware-shipping-methods.md) | Carrier + speed options when ordering hardware. |
| [Configuration](configurations.md) | Per-Reader configuration: tipping, splash screen, offline mode, language. |

## How it fits with PaymentIntent

Terminal does *not* invent a new payment object. The reader collects a `card_present` PaymentMethod, then your server creates a regular [PaymentIntent](../01-core-resources/payment-intents.md) and confirms it with that PM. The reader handles EMV / contactless / chip-and-PIN under the hood.

## Tap to Pay

On supported phones (iPhone with iOS 16+ and Apple developer entitlement, or Android with NFC + Stripe SDK), the phone *is* the reader. No physical hardware needed — the [Reader](readers.md) object still represents the device, type `simulated_wisepad3` becomes `mobile_phone_reader` etc.
