# Example Report: Foundation Models vs AI Applications

**Report ID:** `foundation-vs-application-2026-07`  
**Date:** 2026-07-20  
**Companies referenced:** `anthropic`, `cursor`, `lovable`  
**Status:** illustrative example

## Purpose

Demonstrate how this benchmark separates **AI stack layers** while using one scoring system with within-layer calibration.

## Framing

| Company | Layer | Category | Peer frame |
|---------|-------|----------|------------|
| Anthropic | `model` | Foundation models | Frontier model labs |
| Cursor | `application` | AI developer tools | AI coding / IDE peers |
| Lovable | `application` | AI app builders | Vibe-coding / app-builder peers |

Cursor and Lovable are both application-layer but **different categories**. Equal scores do not mean they compete head-to-head (`extensions.adjacent_products` only).

## Framework scores (calibrated)

| Dimension | Anthropic | Cursor | Lovable | Note |
|-----------|-----------|--------|---------|------|
| `product` | 5 (high) | 4 (high) | 4 (high) | Anthropic in model-lab frame |
| `market` | 4 (medium) | 4 (medium) | 4 (medium) | All capped at 4 without category-level sources |
| `business_model` | 4 (medium) | 4 (high) | 4 (high) | Pricing visibility differs |
| `technology` | 5 (high) | 3 (high) | 3 (high) | Layer-relative; do not rank across layers |
| `growth` | null | null | null | No sourced growth metrics |
| `competitive_position` | 4 (medium) | 3 (medium) | 3 (medium) | Within-layer peer judgments |

## Analytical takeaways

1. **Within-layer first.** Cursor vs Lovable can be compared as application products; Anthropic belongs in a model-lab peer frame.
2. **`market=5` discipline.** Company materials alone no longer justify a 5.
3. **Technology is not absolute.** Application `technology: 3` is not “worse than” model `technology: 5` in a single league table.
4. **Growth stays null** until sourced metrics exist.

## Method notes

- Inputs: `companies/anthropic.json`, `companies/cursor.json`, `companies/lovable.json`
- Calibration: [`../SCHEMA.md`](../SCHEMA.md) Scoring Framework
- Checklist: [`../companies/ENTRY_CHECKLIST.md`](../companies/ENTRY_CHECKLIST.md)

## Limitations

- No category-level market reports attached yet.
- Entry confidence scores are 3–4; growth and funding remain thin.
- Not investment advice.
