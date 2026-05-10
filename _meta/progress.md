# Progress tracker

All 133 Stripe API resources have full deep guides. The project is feature-complete for its first pass.

## Layout

The project uses a **flat structure** (one markdown file per object, sitting directly inside its category folder — no per-object subdirectories):

```
NN-category/
├── README.md          ← category index
├── object-a.md        ← deep guide
├── object-b.md
└── ...
```

## Inventory

- **133 deep object guides** at `<NN-category>/<object>.md` — every Stripe API resource has a full 12-section guide.
- **24 category index READMEs** at `<NN-category>/README.md` — navigable landing for each category.
- **1 root `README.md`** with study path + full category index.
- **7 cross-cutting `_meta/` docs** — api-version, glossary, money-flow, state-machines, webhook-catalog, template, progress, and an index README.

Total: **166 markdown files**, **~1.5 MB of content**, **1275 internal links — all resolve**.

Total: **158 READMEs**, **~1.5 MB of content**.

## Status by category (deep guides per category)

| # | Category | Deep guides | Total content |
|---|---|---|---|
| 01 | Core resources | 18 | ~249 KB |
| 02 | Payment methods | 6 | ~71 KB |
| 03 | Products & catalog | 8 | ~93 KB |
| 04 | Checkout | 1 | ~19 KB |
| 05 | Payment Links | 1 | ~14 KB |
| 06 | Billing | 25 | ~301 KB |
| 07 | Connect | 13 | ~157 KB |
| 08 | Fraud & Radar | 4 | ~42 KB |
| 09 | Issuing | 11 | ~97 KB |
| 10 | Terminal | 8 | ~71 KB |
| 11 | Treasury | 11 | ~111 KB |
| 12 | Identity | 2 | ~28 KB |
| 13 | Reporting | 2 | ~22 KB |
| 14 | Sigma | 1 | ~11 KB |
| 15 | Tax | 5 | ~61 KB |
| 16 | Climate | 3 | ~25 KB |
| 17 | Forwarding | 1 | ~11 KB |
| 18 | Entitlements | 3 | ~29 KB |
| 19 | Webhooks | 1 | ~13 KB |
| 20 | Apps | 1 | ~10 KB |
| 21 | Financial Connections | 5 | ~54 KB |
| 22 | Crypto | 1 | ~13 KB |
| 23 | Agentic commerce | 1 | ~15 KB |
| 24 | Profiles | 1 | ~14 KB |

## How the work was structured

- **Initial pass** (manual): 8 foundational guides (Customer, Charge, PaymentIntent, PaymentMethod, Invoice, CreditNote, Subscription, Connect Account) + all category indexes + all `_meta/` cross-cutting docs.
- **Parallel pass** (20 agents): each agent took a coherent slice of 4-11 objects. All agents read the same template + exemplars before writing, so voice and structure are consistent across categories.

## Quality conventions across all guides

Every object guide follows the same 12-section structure:

1. **What it is** — plain-English definition.
2. **Why it exists** — the problem it solves.
3. **Lifecycle & states** — mermaid `stateDiagram-v2` + per-state semantics.
4. **Anatomy of the object** — fields grouped by purpose, in `Field | Notes` tables.
5. **Relationships** — mermaid `graph LR` + parent/child/optional notes.
6. **Common workflows** — numbered HTTP recipes with code fences.
7. **Webhook events** — `Event | Fires when | Listener typically does` table.
8. **Idempotency, retries & race conditions**.
9. **Test-mode tips** — magic data, CLI commands, test-clock interactions.
10. **Connect considerations** — what changes on a connected account.
11. **Common pitfalls** — concrete "looks right but isn't" mistakes.
12. **Further reading** — links to docs.stripe.com.

Hedging language is used wherever a field/enum is uncertain or version-volatile (especially for newer surfaces: agentic-commerce/tokens, profiles, billing meters/credits, treasury, financial connections).

## Suggested next iterations

- **Code samples in TypeScript / Python / Go** alongside the cURL/HTTP examples.
- **Worked end-to-end recipes**: SaaS subscription with Tax + Customer Portal; Marketplace with Connect destination charges + Application Fees + Refunds; Embedded onboarding with AccountSession; Treasury-funded Issuing card program.
- **Diagrams**: a single big "Stripe object graph" mermaid in `_meta/` that connects every category.
- **Per-version diffs**: when Stripe ships the next API version, add a `## Changes from 2026-04-22.dahlia` section to each affected object.
- **CHANGELOG.md** at root tracking when objects were last reviewed against live Stripe docs.
