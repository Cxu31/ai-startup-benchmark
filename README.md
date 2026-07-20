# AI Startup Benchmark

A structured intelligence benchmark for understanding AI-native companies.

This is a research benchmark and structured dataset — not application source code, not a ChatGPT wrapper, not a ranking leaderboard, and not a marketing site.

## Overview

Information about AI startups is scattered across product sites, pricing pages, GitHub activity, community discussion, hiring pages, and occasional public market signals. Individually, each source is incomplete. Together, they are hard to compare because every write-up uses different categories, different levels of confidence, and different definitions of “AI-native.”

A structured benchmark is useful because it forces the same questions onto every company:

- What is the product, and where does it sit in the stack?
- Who is the customer, and what problem is being sold against?
- How does the business make money?
- How central is AI to the product versus the pitch?
- What evidence supports each claim?

The goal is not a scoreboard for hype. The goal is a shared format for reading AI companies carefully.

## Why This Exists

Most public commentary about AI startups is narrative: launch posts, funding notes, feature lists, and hot takes. Those are useful, but they rarely support systematic comparison.

Understanding why some AI companies compound and others stall usually requires looking across multiple signals at once — product surface, distribution, model dependency, competitive set, and growth evidence — rather than treating any single page or article as complete.

This repository exists to build a structured framework for comparing AI companies across:

- product
- market
- business model
- growth signals

and to keep those comparisons inspectable in git.

## Benchmark Methodology

This project uses **AI-assisted intelligence research**, not AI-generated content as an end product.

| Role | Responsibility |
|------|----------------|
| AI assistance | Helps collect, normalize, and organize publicly available information |
| Humans | Design the schema, categories, evaluation dimensions, and validation rules |
| Humans | Review and validate entries before they are treated as benchmark-ready |

In practice:

1. Public information is gathered and mapped into a fixed schema.
2. Claims that matter are attached to evidence where possible.
3. Scores and judgments are recorded as explicit fields with rationale — not buried in prose.
4. Unknown or weakly evidenced values stay `null` / omitted rather than fabricated.
5. Entries are revised when better sources appear.

AI speeds up collection and structuring. It does not define what “good” means. The schema and evaluation dimensions are human-designed and remain the source of truth for the benchmark.

## Current Benchmark

The initial company set:

| Company | Focus (high level) |
|---------|--------------------|
| Anthropic | Foundation models |
| Cursor | AI-native developer environment |
| Lovable | AI application / product generation |
| Perplexity | AI search / answer products |
| Gamma | AI presentation / content tools |

This set is a starting slice across model labs and application-layer products. The benchmark will expand gradually as the schema stabilizes and more entries meet the evidence bar.

Example profiles and analyses currently live under [`companies/`](./companies/) and [`reports/`](./reports/).

## Data Structure

Each company entry is a versioned JSON profile. The main dimensions:

| Dimension | What it captures |
|-----------|------------------|
| **Product** | What is shipped, stack layer, delivery model, capabilities |
| **Market** | Customer type, persona, category, problem framing |
| **Business Model** | Monetization and pricing visibility |
| **AI Profile** | How central AI is, and how the product depends on models/data |
| **Competitive Position** | Peer set and positioning notes |
| **Growth Signals** | Public traction indicators, when sourced |
| **Evidence** | URLs, dates, snippets, and confidence labels |
| **Scores** | Official `framework_scores` dimensions with written rationale |
| **Confidence Score** | How reliable the overall entry is, given source coverage |

Scores are intended for structured comparison within context, not as a universal ranking system.

Design constraints for every entry:

- **Comparable** — same fields and score axes across companies
- **Traceable** — important claims can point to evidence IDs
- **Versionable** — plain JSON in git, so revisions are reviewable

Field definitions and enums are documented in [`SCHEMA.md`](./SCHEMA.md). Controlled vocabularies and the entry checklist live in [`SCHEMA.md`](./SCHEMA.md#controlled-vocabularies) and [`companies/ENTRY_CHECKLIST.md`](./companies/ENTRY_CHECKLIST.md). The research model is described in [`ARCHITECTURE.md`](./ARCHITECTURE.md). The machine-readable schema is [`companies/company.schema.json`](./companies/company.schema.json).

## Transparency

**Public in this repository**

- benchmark company data
- schema and documentation
- research methodology
- analysis examples

**Private / not published here**

- production collection pipeline
- internal prompts
- proprietary evaluation logic used in production systems

The intent is to share a useful, inspectable intelligence format and sample dataset, while keeping the operational system that produces production-grade updates out of scope for this repo.

## Contributing

Before adding or updating a company file, complete [`companies/ENTRY_CHECKLIST.md`](./companies/ENTRY_CHECKLIST.md).

Feedback is welcome on:

- schema improvements
- new evaluation dimensions
- corrections to benchmark data
- clearer evidence standards

Contributions that improve the framework — definitions, validation rules, or well-sourced company updates — are more valuable than large unverified dumps.

Open an issue describing the proposed change and the sources behind it. Prefer small, checkable diffs.

## About

This benchmark is developed alongside Rivallens, an AI startup intelligence platform focused on analyzing AI products and market signals. The repository stands on its own as an open research artifact: schema, methodology, and structured company data for anyone studying AI-native companies.

## License

Released under the [MIT License](./LICENSE).
