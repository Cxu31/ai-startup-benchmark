# Company Entry Checklist

Use this checklist before marking a company profile as benchmark-ready.

Related: [`SCHEMA.md`](../SCHEMA.md) · [`VOCABULARY.md`](../VOCABULARY.md) · [`company.schema.json`](./company.schema.json)

## 1. Identity

- [ ] `schema_version` is `"2.0.0"`
- [ ] `id` matches filename (`companies/<id>.json`)
- [ ] `name`, `status`, `summary`, `website` filled
- [ ] `product.layer` and `market.category` use controlled vocabulary ([SCHEMA.md](../SCHEMA.md#controlled-vocabularies))
- [ ] `extensions.company_stage` set (`unknown` if unsupported)

## 2. Minimum evidence set

A research-ready entry needs **at least**:

| # | Requirement | Notes |
|---|-------------|-------|
| 1 | `company_website` | Primary product / company page |
| 2 | `pricing_page` **or** product `docs` | Monetization or capability detail |
| 3 | One non-homepage source for non-obvious identity claims | Founders, HQ, legal name, stage — e.g. docs, filings, reputable secondary; omit claim if none |

Rules:

- Do not hang unrelated claims on a single homepage evidence ID.
- Prefer primary sources over press for product and pricing facts.
- If funding / seats / ARR lack a dated source, leave numeric fields `null`.

## 3. Traction signals

Allowed labels only (controlled vocabulary):

- `product_surface`
- `distribution_channels`
- `developer_activity`
- `community_signals`
- `hiring_signals`
- `monetization_signals`

Rules:

- Include a label **only** when sourced.
- If missing, omit the signal (do not invent; optionally note omission in `traction.notes`).
- `community_signals` means public community adoption evidence — not “community support” as a support-plan feature.
- Each signal must have `evidence_ids` that actually support that signal.

## 4. Competitors vs adjacent products

- [ ] `competitors` = **same-category peer set** only
- [ ] Cross-layer or loosely related products go in `extensions.adjacent_products`
- [ ] Do not put a company in `competitors` merely because users might substitute it across categories

## 5. Distribution channels

- [ ] `extensions.distribution_channels` uses the controlled enum only
- [ ] Channel claims are factual or clearly weak; no unsourced “viral adoption” language

## 6. Framework scores

- [ ] All six `framework_scores` keys present
- [ ] Each has `value`, `rationale`, `evidence_ids`
- [ ] Each has `confidence` (`high` | `medium` | `low`) when possible
- [ ] Judgments prefixed with `Judgment:` when helpful
- [ ] Use `null` when evidence is insufficient (especially `growth`)
- [ ] `market` score is **not** `5` if evidence is only the company homepage
- [ ] `technology` scored relative to `product.layer` (within-layer depth)
- [ ] Within-layer peers reviewed together before treating scores as comparable
- [ ] No implication that cross-layer equal scores mean equal outcomes

## 7. Facts vs interpretation

- [ ] Profile fields stay descriptive
- [ ] Interpretation lives in `framework_scores.*.rationale` and reports
- [ ] `extensions.confidence_score` + `confidence_notes` reflect source coverage

## 8. Final pass

- [ ] Validates against `company.schema.json`
- [ ] `last_reviewed` updated (`YYYY-MM-DD`)
- [ ] No legacy `scores.*` block
- [ ] Listed in [`README.md`](./README.md) if added as a benchmark entry

## Quick reject criteria

Reject or keep as stub if any of these are true:

- Only a homepage with no pricing/docs detail
- Invented funding, seats, or ARR
- Mixed peer sets across layers in `competitors`
- Dual scoring systems present
- Growth score without sourced growth evidence
