# Data Center Jobs Calculator

A working tool for estimating the full employment footprint of a data center project, including the operational labor categories that standard economic impact studies omit. Built for RenUSA.

Input a project by megawatts (MW) or building square footage. The model returns jobs across three tiers and lets you compare five published economic models for the indirect/induced effect. It has an internal view (full analysis, all five models, all caveats) and a public/hearing view (conservative, defensible subset).

## Why this exists

Standard data center impact studies count two job categories: temporary construction (large) and permanent on-site staff (small). They miss the recurring operational labor generated over the life of a facility, principally the hardware refresh cycle, on-site "smart hands" contractors, and decommissioning/ITAD work. Virginia's own JLARC report confirms the gap: it cites ~50 workers per 250,000 sq ft, about half of them contractors, and then explicitly excludes those contractors from the official direct-jobs count.

## The three tiers

1. **Permanent on-site jobs** (well-anchored). ~0.30 jobs/MW colocation, ~0.45/MW hyperscale. Cross-checked against JLARC's ~50 workers per 250,000 sq ft (half contract).
2. **Construction jobs** (well-anchored, adjustable). Default 2.0/MW, a defensible midpoint anchored to 2025-2026 announcements.
3. **Recurring operations** (churn dollars anchored, FTE estimated). Annual equipment churn is derived from JLARC's finding that 68% of data center capital is equipment, replaced about every five years. The FTE figure is a transparent assumption, not a sourced number.

## The five indirect/induced models

Selectable in Tier 3 so the tool shows a defensible range rather than a single number.

| Model | Type | Spillover per direct job | Notes |
|---|---|---|---|
| Brookings 2026 | Independent, causal | ~0.6x colo / 1.6x hyper | BLS data, synthetic control. Lowest and hardest to attack. |
| JLARC 2024 | VA government, IMPLAN | ~2.4x blended | Weldon Cooper Center for the Virginia General Assembly. |
| Mangum 2023 | Independent, state | ~3.5x | IMPLAN, excludes construction. Virginia-specific. |
| Ohio River Valley Inst. | Skeptic | ~1.5-2.0x | Cites IMPLAN's own 2-3 state-multiplier guidance. |
| PwC / Data Center Coalition | Industry | ~6-7.5x national | IMPLAN, industry-funded. Hidden in public view. |

## The cross-cutting critique

All four IMPLAN/RIMS models (JLARC, Mangum, ORVI, PwC) add and never subtract; they ignore opportunity cost and, per JLARC's own note, exclude externalities such as carbon and health costs. Brookings is the only model that measures a causal counterfactual, which is why it runs lowest and is the most defensible in a hearing.

## Construction coefficient anchors

| Project | Capacity | Construction jobs | Implied jobs/MW |
|---|---|---|---|
| Bedington, WV (Penzance) | ~600 MW | 1,000+ | ~1.7 |
| CoreWeave, Lancaster PA | ~300 MW | 600 | ~2.0 |
| Stargate, Michigan | ~1,000 MW | 2,500+ | ~2.5 |
| Meta, El Paso TX | ~1,000 MW | 4,000+ (peak) | ~4.0 |

## Key sources

- JLARC, "Data Centers in Virginia" (Report 598), December 2024. Per-facility staffing, 68% equipment capital split, five-year replacement cycle, statewide impact totals, IMPLAN externalities caveat.
- Brookings, "New evidence on data center employment effects" (Bahar and Wright), May 2026.
- Mangum Economics, Virginia data center impact analysis, 2023.
- Ohio River Valley Institute, data center economic development analysis, 2026.
- PwC for the Data Center Coalition, 2023 and 2025 impact studies.
- Project announcements: Gateway, Bedington, CoreWeave, Stargate, Meta (2025-2026).

## Audience views

The public/hearing view hides the industry-funded PwC model and the internal caveats. It never inflates a number; every public figure is a strict subset of the internal view. The headline public figure combines permanent jobs with a conservative independent or government model.

## Usage

Open `index.html` in any browser, or serve via GitHub Pages (Settings > Pages > Source: main, root). No build step, no dependencies. Coefficients are editable in the script block at the bottom of `index.html`.

## Caveats

The square-foot-to-MW conversion (~3,500 sq ft/MW) is loose; the industry estimates by power, not floor area. The Tier 2 FTE figure is an assumption model. Model multipliers are simplified to per-direct-job factors for a quick on-screen comparison; the source studies use fuller input-output structures.
