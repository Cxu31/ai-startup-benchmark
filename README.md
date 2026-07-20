# AI Startup Benchmark

A research benchmark and structured intelligence dataset for understanding AI-native companies.

This repository is a documentation and data project. It is not application source code, not a ChatGPT wrapper, and not a product marketing site.

## Overview

AI startups are hard to understand from public materials alone. Product copy, pricing pages, GitHub activity, hiring pages, community discussion, and occasional market signals are scattered and written for different audiences. The same company can look like infrastructure, a consumer app, or a “platform” depending on which page you read.

Traditional startup databases often emphasize funding rounds, headcount, or category tags. Those fields are useful, but they usually do not capture how an AI product actually works: where it sits in the stack, how strongly it depends on models, how it monetizes usage, or which growth signals are publicly observable.

This project defines a shared structure for collecting and comparing AI-native companies across product positioning, business model, growth signals, competitive context, and related market opportunity notes—so analysis can be inspected, revised, and extended in git.

## Research Questions

The benchmark is designed to support careful comparison within a shared schema. It helps organize publicly available evidence around questions such as:

- How do AI-native companies describe and structure their products?
- How do companies position AI capability relative to the core offering?
- Which business and pricing models are visible in public materials?
- What growth-related signals are publicly observable, when present?
- How do foundation-model labs differ from application-layer AI products on comparable axes?

Answers are provisional and evidence-bound. The dataset is a research artifact for structured comparison, not a forecasting or valuation model.

## Dataset Scope

Each company profile aims to capture structured intelligence across dimensions such as:

| Dimension | Focus |
|-----------|--------|
| Product positioning | What is shipped and how it is described |
| Target users | Primary buyers / users and problem framing |
| Core features | Capabilities that define the product |
| Pricing model | Public pricing shape and visibility |
| Business model | How monetization appears to work |
| Market category | Peer category used for comparison |
| Competitive landscape | Same-category peers and adjacent products |
| Growth signals | Public traction indicators when sourced |
| Technology indicators | Model dependency, stack layer, and related signals |
| Evidence & scores | Sources, confidence, and structured judgments |

Unknown or unavailable fields are left empty or set to `null`. Missing or unavailable information is represented as `null` rather than estimated. Incomplete records are preferred over fabricated precision.

## Dataset Structure

Company profiles live as versioned JSON files under [`companies/`](./companies/), one file per company (`companies/<id>.json`).

**Simplified example** (illustrative only; not a complete record). Real profiles include additional optional fields such as `funding`, `team`, `tags`, and `extensions`:

```json
{
  "schema_version": "2.0.0",
  "id": "example-ai",
  "name": "Example AI",
  "legal_name": null,
  "website": "https://example.ai",
  "founded_year": 2024,
  "status": "active",
  "summary": "Short neutral description of the company and product.",
  "product": {
    "one_liner": "One-line product description",
    "layer": "application",
    "delivery": "saas",
    "description": "Longer product description from public materials.",
    "key_capabilities": ["capability-a", "capability-b"]
  },
  "market": {
    "customer_type": "developer",
    "primary_persona": "Primary user or buyer",
    "category": "AI developer tools",
    "problem": "Problem the product addresses",
    "geo_focus": ["global"]
  },
  "business_model": {
    "primary": "subscription",
    "notes": null,
    "pricing_visibility": "public"
  },
  "ai_profile": {
    "centrality": "core",
    "dependency": "mixed",
    "model_strategy": null,
    "data_advantage": null,
    "notes": null
  },
  "traction": {
    "signals": [
      {
        "label": "product_surface",
        "value": "Public product site is live",
        "as_of": "2026-07-20",
        "evidence_ids": ["ev-001"]
      }
    ],
    "notes": null
  },
  "competitors": ["peer-company-a"],
  "framework_scores": {
    "product": {
      "value": 4,
      "rationale": "Judgment: brief rationale",
      "evidence_ids": ["ev-001"],
      "confidence": "medium"
    },
    "market": {
      "value": 4,
      "rationale": "Judgment: brief rationale",
      "evidence_ids": ["ev-001"],
      "confidence": "medium"
    },
    "business_model": {
      "value": 4,
      "rationale": "Judgment: brief rationale",
      "evidence_ids": ["ev-001"],
      "confidence": "high"
    },
    "technology": {
      "value": 3,
      "rationale": "Judgment: brief rationale",
      "evidence_ids": ["ev-001"],
      "confidence": "medium"
    },
    "growth": {
      "value": null,
      "rationale": "Not scored: insufficient public growth evidence",
      "evidence_ids": [],
      "confidence": "high"
    },
    "competitive_position": {
      "value": 3,
      "rationale": "Judgment: brief rationale",
      "evidence_ids": ["ev-001"],
      "confidence": "medium"
    }
  },
  "evidence": [
    {
      "id": "ev-001",
      "type": "company_website",
      "url": "https://example.ai",
      "title": "Example homepage",
      "publisher": "Example AI",
      "published_at": null,
      "accessed_at": "2026-07-20",
      "snippet": "Short source note",
      "confidence": "high"
    }
  ],
  "last_reviewed": "2026-07-20"
}
```

Field definitions, enums, evidence rules, and scoring dimensions are documented in:

- [`SCHEMA.md`](./SCHEMA.md) — methodology and field definitions
- [`VOCABULARY.md`](./VOCABULARY.md) — controlled vocabularies
- [`companies/company.schema.json`](./companies/company.schema.json) — JSON Schema (`schema_version` `2.0.0`)
- [`ARCHITECTURE.md`](./ARCHITECTURE.md) — layered research model

Official scores use `framework_scores` (product, market, business_model, technology, growth, competitive_position). Scores are designed for contextual comparison within this dataset and should not be interpreted as universal rankings.

## Benchmark Methodology

**Selection.** The initial set spans foundation-model and application-layer AI companies with enough public product surface to map into the schema. Coverage will expand as entries meet the evidence bar.

**Collection.** Information is gathered from public sources such as company websites, pricing pages, documentation, and reputable secondary references when needed for identity fields.

**Structuring.** Claims are mapped into fixed fields. Important statements should cite evidence IDs. Judgments are separated from descriptive facts and recorded in score rationales.

**Quality.** Entries follow [`companies/ENTRY_CHECKLIST.md`](./companies/ENTRY_CHECKLIST.md): minimum evidence set, controlled labels for traction and distribution channels, peer-set rules for competitors, and calibration rules for scores. Human review defines schema and validation standards; AI assistance may help collect and organize public information.

This methodology supports reproducibility and review. It does not claim laboratory measurement accuracy or complete market coverage.

## Limitations

- **Not a ranking system.** This project is not a ranking system. Profiles and scores are for contextual comparison within this dataset, not universal rankings or “best company” claims.
- **Public-source dependency.** Entries rely on publicly available materials. Private metrics, contracts, and internal roadmaps are out of scope.
- **Incomplete coverage.** The initial company set is small and illustrative. Absence from the dataset is not a quality judgment.
- **Null over estimation.** Missing or unavailable information is represented as `null` rather than estimated.
- **Judgment vs measurement.** `framework_scores` are structured human judgments with rationales and evidence links; they are not audited performance metrics.

## Example Companies

The current dataset is a small cross-category sample. It demonstrates the benchmark framework and schema in practice; it is not a comprehensive ranking or leaderboard.

Profiles currently included:

| Company | Category |
|---------|----------|
| [Anthropic](./companies/anthropic.json) | Foundation models |
| [Cursor](./companies/cursor.json) | AI developer tools |
| [Lovable](./companies/lovable.json) | AI app builders |
| [Perplexity](./companies/perplexity.json) | AI search |
| [Gamma](./companies/gamma.json) | AI presentation tools |

Cross-company notes live under [`reports/`](./reports/).

Only companies with corresponding JSON files under [`companies/`](./companies/) are listed above.

## Use Cases

Possible readers and users:

- AI founders comparing product and monetization patterns
- Researchers studying AI-native company structure
- Investors seeking an inspectable public-data framework (not investment advice)
- Product strategists mapping categories and peer sets
- Developers building AI applications who want clearer category language

## Relationship with Rivallens

Rivallens is an AI-powered analysis system that explores startup products through structured signals such as business models, pricing, competition, and growth indicators. This repository focuses on the benchmark and structured dataset.

## Roadmap

- Additional AI company profiles that meet the evidence checklist
- Incremental schema improvements (additive fields, clearer rubrics)
- Richer structured signals where public sources allow
- Community contributions via reviewed, sourced updates

## Contributing

Before adding or updating a company file, complete [`companies/ENTRY_CHECKLIST.md`](./companies/ENTRY_CHECKLIST.md).

Prefer small, checkable diffs with sources. Schema and vocabulary changes should be documented in [`SCHEMA.md`](./SCHEMA.md) / [`VOCABULARY.md`](./VOCABULARY.md).

## License

Released under the [MIT License](./LICENSE).
