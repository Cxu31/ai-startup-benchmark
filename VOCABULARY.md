# Controlled Vocabularies

Canonical values for benchmark company entries. Full methodology: [`SCHEMA.md`](./SCHEMA.md#controlled-vocabularies).

## `market.category`

| Value | Typical `product.layer` |
|-------|-------------------------|
| `Foundation models` | `model` |
| `AI developer tools` | `application` |
| `AI app builders` | `application` |
| `AI search` | `application` |
| `AI presentation tools` | `application` |
| `AI infrastructure` | `infrastructure` |
| `AI platforms` | `platform` |
| `Other` | any |

## `extensions.distribution_channels`

`direct_web` · `product_led` · `developer_api` · `enterprise_sales` · `templates` · `public_publish` · `open_source` · `marketplace` · `partnership` · `content` · `other`

## Traction `label` values

`product_surface` · `distribution_channels` · `developer_activity` · `community_signals` · `hiring_signals` · `monetization_signals`

Omit unsourced labels.

## Competitors vs adjacent

| Field | Rule |
|-------|------|
| `competitors` | Same-category peer set only |
| `extensions.adjacent_products` | Cross-category / cross-layer substitutes or complements |

## `framework_scores` keys

`product` · `market` · `business_model` · `technology` · `growth` · `competitive_position`

Each: `value` (1–5 or `null`), `rationale`, `evidence_ids`, recommended `confidence` (`high` \| `medium` \| `low`).
