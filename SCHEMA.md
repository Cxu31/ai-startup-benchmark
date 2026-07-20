# AI Startup Benchmark Schema

This document defines the methodology and data model used to analyze and compare AI-native companies in this benchmark.

It is the conceptual contract for company entries. The machine-readable JSON Schema lives at [`companies/company.schema.json`](./companies/company.schema.json). Company files live in [`companies/`](./companies/).

This schema exists so different companies can be read with the same questions, the same evidence standards, and the same scoring axes — not so every narrative can invent its own vocabulary.

## Design Principles

The benchmark is designed to be:

| Principle | Meaning |
|-----------|---------|
| **Comparable** | Every company is described with the same sections and score dimensions. Differences should reflect the company, not inconsistent writing. |
| **Traceable** | Important claims point to evidence: source, type, and confidence. Judgments are labeled as judgments. |
| **Versionable** | Profiles are plain JSON in git. Revisions are reviewable; older states remain inspectable. |

Secondary rules follow from those three:

- Prefer structured fields over freeform essays.
- Prefer public sources over private anecdotes.
- Prefer `null` / unknown over invented precision.
- Prefer small, sourced updates over large unverified dumps.

## Company Profile

Identity and placement fields used to locate a company in the benchmark.

| Field | Description |
|-------|-------------|
| `company_name` | Display name of the company. |
| `category` | High-level category label used for grouping (e.g. foundation models, AI developer tools, AI search). |
| `product_layer` | Where the company primarily sits in the AI stack. |
| `company_stage` | Approximate maturity band based on public signals (not a valuation claim). |

### `product_layer` values

| Value | Meaning |
|-------|---------|
| `infrastructure` | Compute, data, eval, or tooling primarily for builders |
| `model` | Foundation or specialized models |
| `platform` | APIs, orchestration, or developer platforms |
| `application` | End-user or vertical software |
| `services` | Services-heavy delivery wrapped around AI |
| `other` | Does not fit cleanly; explain in notes |

### `company_stage` values

| Value | Meaning |
|-------|---------|
| `pre_seed` / `seed` | Early product and early distribution |
| `series_a` / `series_b` / `growth` | Later private stages when publicly reported |
| `public` | Public company |
| `acquired` / `shutdown` / `stealth` / `unknown` | Non-standard or unclear states |

Use stage only when supported by public information. If stage is unclear, use `unknown` rather than inferring from vibes.

### JSON mapping

| Conceptual field | Typical JSON path |
|------------------|-------------------|
| `company_name` | `name` |
| `category` | `market.category` and/or `tags` |
| `product_layer` | `product.layer` |
| `company_stage` | `extensions.company_stage` until promoted to a top-level field |

Supporting identity fields in JSON also include `id`, `website`, `founded_year`, `hq`, `status`, and `summary`.

## Product Analysis

What the company ships, for whom, and against which problem.

| Field | Description |
|-------|-------------|
| `product_description` | Neutral description of the product surface and workflow. Avoid marketing adjectives. |
| `core_features` | Short list of capabilities that define the product, not an exhaustive changelog. |
| `target_users` | Primary users or buyers the product is built for. |
| `user_problem` | The job-to-be-done or pain the product claims to address. |

Good product entries answer:

1. What does a user actually do in the product?
2. What would be missing if the AI component were removed?
3. Is this an IDE, search product, model API, workflow app, or something else?

### JSON mapping

| Conceptual field | Typical JSON path |
|------------------|-------------------|
| `product_description` | `product.description` (+ `product.one_liner`) |
| `core_features` | `product.key_capabilities` |
| `target_users` | `market.primary_persona` (+ `market.customer_type`) |
| `user_problem` | `market.problem` |

Also record delivery shape in `product.delivery` (`api`, `saas`, `open_source`, `hardware`, `marketplace`, `hybrid`, `other`).

## Controlled Vocabularies

Use these values for cross-company consistency. Prefer omitting a field/signal over inventing a near-match string.

### `market.category`

Canonical strings (exact match preferred):

| Value | Typical `product.layer` | Examples in this repo |
|-------|-------------------------|------------------------|
| `Foundation models` | `model` | Anthropic |
| `AI developer tools` | `application` | Cursor |
| `AI app builders` | `application` | Lovable |
| `AI search` | `application` | — |
| `AI presentation tools` | `application` | — |
| `AI infrastructure` | `infrastructure` | — |
| `AI platforms` | `platform` | — |
| `Other` | any | Use sparingly; explain in notes |

If a company spans categories, pick the **primary** buying category and note overlap in `extensions.market_position`.

### `extensions.distribution_channels`

Array of zero or more:

| Value | Meaning |
|-------|---------|
| `direct_web` | Primary acquisition via company website / product signup |
| `product_led` | Bottom-up PLG / self-serve expansion inside product |
| `developer_api` | Distribution via API / developer platform |
| `enterprise_sales` | Sales-led or enterprise motion |
| `templates` | Template gallery or start-from-template distribution |
| `public_publish` | Publicly published user projects as discovery surface |
| `open_source` | Open-source project as acquisition funnel |
| `marketplace` | App store / cloud marketplace |
| `partnership` | Channel or platform partnerships |
| `content` | Docs, content, or community content as primary channel |
| `other` | Explain in `extensions.market_position` or traction notes |

### Traction `label` values

Only these labels may appear in `traction.signals[]`:

| Label | Include when |
|-------|----------------|
| `product_surface` | Live public product / docs surfaces exist |
| `distribution_channels` | Observable channel pattern from public sources |
| `developer_activity` | Public developer artifacts (API docs, SDKs, Git sync, OSS) |
| `community_signals` | Public community adoption evidence (forums, notable adoption threads) — **not** “community support” as a ticket tier |
| `hiring_signals` | Public careers / hiring mix evidence |
| `monetization_signals` | Public pricing, plans, or packaging evidence |

If a label cannot be sourced, **omit it**.

### `competitors` vs `extensions.adjacent_products`

| Field | Rule |
|-------|------|
| `competitors` | Same `market.category` (or same competitive peer set). Buyers compare these directly. |
| `extensions.adjacent_products` | Cross-category or cross-layer substitutes / complements. Useful context, not peer scoring fodder. |

Examples:

- Lovable peers: other AI app builders → `competitors`
- Cursor next to Lovable → `extensions.adjacent_products` (IDE vs app builder)
- Anthropic peers: other foundation-model labs → `competitors`

Use kebab-case IDs when the peer may join this dataset; otherwise a stable public name is acceptable.

## Market Analysis

How the company sits in a competitive landscape.

| Field | Description |
|-------|-------------|
| `market_category` | The market bucket used for peer comparison. |
| `market_position` | Concise statement of how the company positions itself within that category. |
| `competitors` | Same-category peer set only (see controlled vocabulary). |
| `differentiation` | Claimed or observed differences that matter to buyers — not slogan text. |

Market analysis should separate:

- **Category** — what market is this?
- **Position** — where does this company sit inside it?
- **Differentiation** — why might a buyer choose it over peers?

If differentiation is mostly marketing language with weak evidence, say so and lower confidence.

### JSON mapping

| Conceptual field | Typical JSON path |
|------------------|-------------------|
| `market_category` | `market.category` |
| `market_position` | `extensions.market_position` |
| `competitors` | `competitors` |
| adjacent / cross-layer products | `extensions.adjacent_products` |
| `differentiation` | `extensions.differentiation` and/or `framework_scores.competitive_position` rationale |

## Business Model

How the company appears to make money from public information.

| Field | Description |
|-------|-------------|
| `revenue_model` | Primary monetization pattern. |
| `pricing_strategy` | How pricing is presented: seats, usage, freemium gates, enterprise contracts, etc. |
| `monetization_signals` | Public clues that monetization is working or changing (plan launches, usage pricing, enterprise packaging). |

Suggested `revenue_model` values:

`subscription`, `usage`, `seat`, `license`, `marketplace_take_rate`, `services`, `ads`, `freemium`, `open_core`, `mixed`, `unclear`

Do not invent ARR, take rates, or margin claims. If pricing is not public, record visibility as limited and keep numeric claims empty.

### JSON mapping

| Conceptual field | Typical JSON path |
|------------------|-------------------|
| `revenue_model` | `business_model.primary` |
| `pricing_strategy` | `business_model.notes` + `business_model.pricing_visibility` |
| `monetization_signals` | `traction.signals` filtered to monetization-related labels |

## AI Profile

How AI actually shows up in the product — not how prominently it appears in marketing.

| Field | Description |
|-------|-------------|
| `AI capability` | What AI does in the product: generation, retrieval, coding agents, ranking, automation, etc. |
| `model usage` | Whether the company owns models, fine-tunes, wraps APIs, orchestrates tools, or builds around proprietary data loops. |
| `AI-native characteristics` | Signs that AI is structural to the product (workflow redesign, eval loops, model routing, data flywheels) versus bolted-on features. |

Useful distinctions:

| Pattern | Meaning |
|---------|---------|
| `owns_models` | Trains / serves primary models |
| `fine_tunes` | Adapts base models for a domain |
| `api_wrapper` | Thin product over third-party model APIs |
| `orchestration` | Agents, tools, workflows, routing on top of models |
| `data_network` | Advantage depends on proprietary data/feedback loops |
| `mixed` | Combination of the above |
| `unclear` | Insufficient public evidence |

`api_wrapper` is not an insult; it is a dependency description. Many useful products are wrappers with strong distribution or UX. The schema should make that dependency visible.

### JSON mapping

| Conceptual field | Typical JSON path |
|------------------|-------------------|
| `AI capability` | `ai_profile.notes` / product capabilities |
| `model usage` | `ai_profile.dependency` + `ai_profile.model_strategy` |
| `AI-native characteristics` | `ai_profile.centrality` + `ai_profile.data_advantage` |

`ai_profile.centrality` values: `core`, `embedded`, `feature`, `marketing`, `unclear`.

## Growth Signals

Public indicators that distribution or adoption may be compounding. These are signals, not audited metrics.

| Field | Description |
|-------|-------------|
| `community signals` | Discussion intensity, community presence, notable public adoption conversations. |
| `developer activity` | GitHub / open-source activity, SDK adoption clues, developer chatter. |
| `hiring signals` | Role mix and hiring velocity when publicly visible (e.g. GTM vs research vs infra). |
| `distribution channels` | How the product appears to spread: bottom-up PLG, marketplace, partnerships, sales-led, content, etc. |

Rules:

- Record the signal and date when possible.
- Do not treat a single viral post as durable growth.
- Do not convert soft signals into fake precision (e.g. inventing MAU).

### JSON mapping

| Conceptual field | Typical JSON path |
|------------------|-------------------|
| growth fields above | `traction.signals[]` using **only** controlled traction labels |
| distribution notes | `extensions.distribution_channels` (controlled enum) and/or `framework_scores.growth` rationale |

## Evidence System

Every important claim should be able to answer: **says who, from where, and how sure are we?**

For material claims, attach:

| Field | Description |
|-------|-------------|
| `evidence source` | URL or citable public reference |
| `evidence type` | What kind of source it is |
| `confidence score` | Reliability of that evidence item or claim |

### Evidence types

Suggested values:

- `company_website`
- `pricing_page`
- `docs`
- `github`
- `job_posting`
- `blog_post`
- `news_article`
- `interview`
- `regulatory_filing`
- `dataset_release`
- `other`

### Confidence

| Level | Use when |
|-------|----------|
| `high` | Primary source, recent, unambiguous |
| `medium` | Credible secondary source, or primary source with ambiguity |
| `low` | Thin, outdated, conflicting, or indirectly inferred |

### Why represent uncertainty

Guessing creates false comparability. A fabricated funding number or seat count looks more precise than a honest `null`, and then pollutes every later comparison.

The benchmark prefers:

- `null` for unknown quantities
- `unknown` / `unclear` enums when classification is unresolved
- explicit low confidence when a claim is weak but still useful to record

Uncertainty is part of the data model, not a failure of the entry.

### JSON mapping

Evidence items live in `evidence[]`:

```json
{
  "id": "ev-001",
  "type": "company_website",
  "url": "https://example.com",
  "title": "Source title",
  "publisher": "Publisher",
  "published_at": "2026-01-15",
  "accessed_at": "2026-07-20",
  "snippet": "Optional short excerpt or paraphrase",
  "confidence": "medium"
}
```

Claims and scores reference evidence through `evidence_ids`.

Entry-level reliability can be summarized as a **confidence score** for the whole profile (source coverage × recency × conflict). Until formalized as a top-level field, record it under `extensions.confidence_score` (`1–5` or `null`) with a short note.

## Scoring Framework

Official scoring object: **`framework_scores`**.

Scores are **structured judgments**, not measurements. They make comparisons explicit and reviewable. Do not invent a parallel scoring block.

### Official dimensions

| Key | Dimension | Core question |
|-----|-----------|---------------|
| `product` | Product | Is there a clear, coherent product users can understand and adopt? |
| `market` | Market | Is the category real, reachable, and large enough to matter? |
| `business_model` | Business Model | Is there a plausible monetization path visible from public signals? |
| `technology` | Technology | How deep is the technical system relative to the product claim? |
| `growth` | Growth | Do public signals suggest compounding distribution or usage? |
| `competitive_position` | Competitive Position | How defensible or differentiated does the company look versus peers? |

### Scale

| Value | Meaning |
|-------|---------|
| `1` | Weak / unclear |
| `2` | Below average |
| `3` | Mixed / average |
| `4` | Strong |
| `5` | Exceptional (rare) |
| `null` | Not scored — evidence insufficient |

Each dimension object must include:

- `value` — integer 1–5, or `null`
- `rationale` — short, specific; prefix judgments with `Judgment:` when helpful
- `evidence_ids` — links to `evidence[]` when possible

Optional but recommended:

- `confidence` — `high` | `medium` | `low` | `null` — how reliable this dimension score is given the attached evidence

### Scoring criteria

#### `product`

| Score | Criteria |
|-------|----------|
| 1 | Unclear what is shipped; product surface is vague or contradictory |
| 2 | Product exists but workflow, buyer, or scope is hard to explain |
| 3 | Understandable product with mixed clarity on depth or completeness |
| 4 | Clear product, coherent workflows, adoptable by the stated user |
| 5 | Unusually sharp product definition and packaging for its category |

#### `market`

| Score | Criteria |
|-------|----------|
| 1 | Category is unclear, tiny, or not a real buying motion |
| 2 | Niche or weakly formed market with limited evidence of demand |
| 3 | Recognizable category with mixed size/accessibility signals |
| 4 | Clear, active market with identifiable buyers and peers |
| 5 | Large, structurally important category with strong demand evidence |

**Evidence rule for `market`:** A company homepage or product page alone is **not** sufficient for `value: 5`. Prefer category-level sources (industry coverage naming multiple peers, credible market maps, or multiple independent buyer/peer signals). If only company materials support “this category exists,” cap at **4** or use `null`.

#### `business_model`

| Score | Criteria |
|-------|----------|
| 1 | No visible monetization path |
| 2 | Monetization mentioned but weak, opaque, or implausible from public info |
| 3 | Plausible model with limited pricing/packaging visibility |
| 4 | Clear public monetization path (e.g. priced plans, usage billing) |
| 5 | Unusually clear and credible monetization design for the category |

#### `technology`

| Score | Criteria |
|-------|----------|
| 1 | Little evidence the tech matches the claim; likely thin wrapper without product depth |
| 2 | Mostly generic API usage with minimal system differentiation |
| 3 | Meaningful product/systems work (orchestration, UX, data, eval) without owning frontier models |
| 4 | Substantial technical depth relative to peers in the same layer |
| 5 | Rare depth — e.g. frontier model ownership or uniquely hard systems advantage |

Score relative to the company's **layer**. An application should not be punished for not training foundation models; it should be scored on depth appropriate to application-layer claims.

#### `growth`

| Score | Criteria |
|-------|----------|
| 1 | Public signals suggest stagnation, decline, or no adoption path |
| 2 | Weak or stale growth evidence |
| 3 | Mixed or early signals; direction unclear |
| 4 | Multiple sourced signals of compounding usage or distribution |
| 5 | Rare, well-evidenced breakout growth |

If there are no sourced growth metrics or durable proxies, use `null` rather than guessing.

#### `competitive_position`

| Score | Criteria |
|-------|----------|
| 1 | No clear differentiation; easily substituted |
| 2 | Weak position in a crowded set |
| 3 | Visible contender with uncertain defensibility |
| 4 | Clear differentiation and credible barriers versus named peers |
| 5 | Dominant or uniquely defensible position (rare; requires strong evidence) |

### Calibration rules

1. **Within-layer first.** Calibrate `application` companies against each other (e.g. Cursor vs Lovable) before comparing to `model` labs (e.g. Anthropic). Do not treat cross-layer score equality as “equally strong businesses.”
2. **`5` is rare.** Default strong-but-normal outcomes to `4`. Reserve `5` for exceptional, well-evidenced cases.
3. **`market` discipline.** Homepage-only → max `4` (or `null`). `5` needs category-level evidence.
4. **`technology` is layer-relative.** Application orchestration depth tops out differently than frontier model ownership; state the peer frame in the rationale.
5. **Prefer `null` over weak numbers** for `growth` and weakly evidenced `competitive_position`.
6. **Per-dimension `confidence`.** High = primary sources directly support the judgment; medium = partial/indirect; low = thin. A high `value` with low `confidence` is a smell — usually lower the value or gather evidence.
7. **No cross-layer league tables.** Reports may compare profiles across layers; they should not rank companies from different layers by averaging `framework_scores`.

### Deprecated: legacy `scores.*`

Removed in schema **2.0.0**:

- `ai_centrality`
- `moat_clarity`
- `distribution_strength`
- `technical_depth`
- `market_timing`
- `execution_signal`

Also removed: temporary `extensions.framework_scores`.

Migration map (for reading old commits only):

| Legacy field | Nearest official dimension |
|--------------|----------------------------|
| `ai_centrality` | (absorbed into product / technology / profile fields; not a standalone score) |
| `technical_depth` | `technology` |
| `market_timing` | `market` |
| `moat_clarity` | `competitive_position` |
| `distribution_strength` | `growth` / distribution notes |
| `execution_signal` | `growth` |

Do not keep both systems in the same file.

### JSON shape

```json
"framework_scores": {
  "product": {
    "value": 4,
    "rationale": "Judgment: coherent product with clear core workflows.",
    "evidence_ids": ["ev-001"],
    "confidence": "high"
  },
  "market": { "value": 4, "rationale": "...", "evidence_ids": ["ev-001"], "confidence": "medium" },
  "business_model": { "value": 4, "rationale": "...", "evidence_ids": ["ev-002"], "confidence": "high" },
  "technology": { "value": 3, "rationale": "...", "evidence_ids": ["ev-001"], "confidence": "high" },
  "growth": { "value": null, "rationale": "Not scored: no sourced growth metrics.", "evidence_ids": [], "confidence": "high" },
  "competitive_position": { "value": 3, "rationale": "...", "evidence_ids": ["ev-001"], "confidence": "medium" }
}
```

### Calibration notes

See **Calibration rules** above. Summary:

- Prefer `null` over a weakly evidenced number for `growth` and weakly evidenced `competitive_position`.
- A high `product` score does not imply a high `technology` score.
- Equal scores across different `product.layer` values are not league-table ties.
- Rubrics may tighten in later schema versions; do not silently reinterpret historical values.

## Data Quality Principles

1. **Prefer public evidence.** Benchmark entries should be reconstructible from sources others can check.
2. **Separate facts from interpretation.** Facts go in profile fields and evidence. Interpretation goes in score rationales and reports.
3. **Use `null` for unknown information.** Missing data is allowed. Fake precision is not.
4. **Avoid unsupported claims.** If a statement cannot be sourced or clearly marked as judgment, omit it.
5. **Date what you can.** Traction and pricing claims decay quickly; record `as_of` / `accessed_at`.
6. **Keep summaries neutral.** Opinions belong in scores and reports, not in identity blurbs.
7. **Correct in public.** When wrong, update the JSON and leave the history in git.

## File Conventions

| Rule | Detail |
|------|--------|
| Path | `companies/<id>.json` |
| `id` | kebab-case ASCII; must match filename |
| Encoding | UTF-8 |
| Indent | 2 spaces preferred |
| `schema_version` | Currently `"2.0.0"` |
| `last_reviewed` | ISO date `YYYY-MM-DD` |

## Schema Versioning

- **Patch** (`2.0.x`): documentation clarifications only
- **Minor** (`2.x.0`): additive optional fields
- **Major** (`x.0.0`): breaking renames, removals, or score-dimension changes

### Migration notes

| Version | Change |
|---------|--------|
| `1.0.0` | Initial schema; legacy `scores.*` dimensions |
| `2.0.0` | Official `framework_scores` only; legacy `scores.*` and `extensions.framework_scores` removed |

Breaking changes should include a short migration note in this file.

## Related Documents

- [`ARCHITECTURE.md`](./ARCHITECTURE.md) — layered research model
- [`README.md`](./README.md) — project positioning
- [`companies/ENTRY_CHECKLIST.md`](./companies/ENTRY_CHECKLIST.md) — entry quality checklist
- [`companies/company.schema.json`](./companies/company.schema.json) — machine-readable validation schema
- [`reports/`](./reports/) — cross-company analyses using these fields
