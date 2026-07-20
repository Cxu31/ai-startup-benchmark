# Architecture

This document describes the **AI Startup Intelligence Framework** used by this benchmark.

The framework turns messy public information about AI startups into comparable, versionable records.

## Purpose

Researchers, operators, and investors often describe AI startups with incompatible language:

- “AI-native” vs “AI-enabled”
- “platform” vs “application”
- “defensible” vs “feature”

This benchmark defines a shared vocabulary and a layered data model so companies can be compared on the same axes.

## Layers

```text
┌─────────────────────────────────────────────┐
│  Layer 4 — Reports                          │
│  Cross-company analysis, themes, rankings   │
├─────────────────────────────────────────────┤
│  Layer 3 — Scores & Judgments               │
│  Structured ratings with rationale          │
├─────────────────────────────────────────────┤
│  Layer 2 — Evidence                         │
│  Sources, quotes, dates, confidence         │
├─────────────────────────────────────────────┤
│  Layer 1 — Company Profile (facts)          │
│  Identity, product, market, traction signals│
└─────────────────────────────────────────────┘
```

### Layer 1 — Company Profile

Canonical facts about the company: name, founding year, HQ, product summary, target customer, business model, and similar baseline fields.

These fields should be **observable** or **widely reported**, not speculative.

### Layer 2 — Evidence

Each non-trivial claim can attach evidence:

- `url`
- `title`
- `published_at`
- `accessed_at`
- `snippet`
- `confidence` (`high` | `medium` | `low`)

Evidence prevents the dataset from becoming a pile of unsourced opinions.

### Layer 3 — Scores & Judgments

Normalized dimensions used for comparison (`framework_scores`):

| Dimension | Question it answers |
|-----------|---------------------|
| `product` | Is there a clear, coherent product users can understand and adopt? |
| `market` | Is the category real, reachable, and large enough to matter? |
| `business_model` | Is there a plausible monetization path from public signals? |
| `technology` | How deep is the technical system relative to the product claim? |
| `growth` | Do public signals suggest compounding distribution or usage? |
| `competitive_position` | How defensible or differentiated does the company look versus peers? |

Scores are **judgments**. They must include a short rationale and preferably evidence links. Rubrics live in [`SCHEMA.md`](./SCHEMA.md).

### Layer 4 — Reports

Reports synthesize multiple company profiles into themes:

- category maps
- competitive clusters
- “wrapper vs foundation” analyses
- vertical AI landscapes

Reports live in `reports/` as Markdown (and optionally accompanying JSON summaries).

## Entity model

Primary entities:

1. **Company** — one JSON file in `companies/`
2. **EvidenceItem** — nested under company claims or scores
3. **ScoreDimension** — named rating with rationale
4. **Report** — Markdown analysis referencing company IDs

### Company identity

Each company has a stable `id` in kebab-case, matching the filename:

```text
companies/anthropic.json  →  "id": "anthropic"
companies/perplexity.json →  "id": "perplexity"
```

## Analysis workflow

Recommended research loop:

1. **Collect** public facts into the company profile.
2. **Attach evidence** for non-obvious claims.
3. **Score** using the shared dimensions.
4. **Compare** across peer companies in a report.
5. **Revise** when new evidence appears (git history preserves prior states).

## Quality bar

A company profile is considered research-ready when:

- required schema fields are present
- product and customer are described clearly
- at least three evidence items support key claims
- score dimensions include rationale text
- sources are dated or marked as undated with lower confidence

## Extensibility

The schema can grow, but extensions should:

- remain backward compatible when possible
- document new fields in `SCHEMA.md`
- avoid company-specific one-off keys unless namespaced under `extensions`

## Out of scope

This architecture deliberately excludes:

- runtime agents or scrapers
- private CRM / deal-flow systems
- proprietary valuation models
- prompt templates for automated analysis

The value of the project is a **shared, inspectable intelligence format**, not automation.
