# Data Center Jobs Calculator

A working tool for estimating the full employment footprint of a data center project, including the operational labor categories that standard economic impact studies omit. Built for RenUSA.

**Live:** https://dave-renusa.github.io/dcjobs/ (redirects to `model.html`). Current version: **v2.0 (September 2026)**.

Input a project by megawatts (MW) or building square footage. The model returns jobs across three tiers, construction job-years, capital per job, a county-level check and annual fiscal figures, and lets you compare five published economic models for the indirect/induced effect. It has an internal view (full analysis, all five models, all caveats) and a public/hearing view (conservative, defensible subset).

## Why this exists

Standard data center impact studies count two job categories: temporary construction (large) and permanent on-site staff (small). They miss the recurring operational labor generated over the life of a facility, principally the hardware refresh cycle, on-site "smart hands" contractors, and decommissioning/ITAD work. Virginia's own JLARC report confirms the gap: it cites ~50 workers per 250,000 sq ft, about half of them contractors, and then explicitly excludes those contractors from the official direct-jobs count.

## The three tiers

1. **Permanent on-site jobs** (well-anchored). ~0.30 jobs/MW colocation, ~0.45/MW hyperscale, ~0.20/MW AI training campus (Meta Hyperion: 1,000 permanent jobs on ~5 GW). Cross-checked against JLARC's ~50 workers per 250,000 sq ft (half contract).
2. **Construction jobs** (well-anchored, adjustable). Default 2.0/MW, a defensible midpoint anchored to 2025-2026 announcements.
3. **Recurring operations** (churn dollars anchored, FTE estimated). Annual equipment churn is derived from JLARC's finding that 68% of data center capital is equipment, replaced about every five years. The FTE figure is a transparent assumption, not a sourced number.

## The five indirect/induced models

Selectable in Tier 3 so the tool shows a defensible range rather than a single number.

| Model | Type | Spillover per direct job | Notes |
|---|---|---|---|
| Brookings 2026 | Independent, causal | ~0.6x colo / 1.6x hyper | BLS data, synthetic control. Lowest and hardest to attack. Revised ~Aug 2026 with an expanded sample; multipliers here are from the May version and need re-verification. |
| JLARC 2024 | VA government, IMPLAN | ~2.4x blended | Weldon Cooper Center for the Virginia General Assembly. |
| Mangum 2023 | Independent, state | ~3.5x | IMPLAN, excludes construction. Virginia-specific. |
| Ohio River Valley Inst. | Skeptic | ~1.5-2.0x | Cites IMPLAN's own 2-3 state-multiplier guidance. |
| PwC / Data Center Coalition 2026 | Industry | ~4.5x national | IMPLAN, 2024 data, industry-funded. Down from ~6x in the 2023 study. Optional state multiplier override. Hidden in public view. |

## The cross-cutting critique

All four IMPLAN/RIMS models (JLARC, Mangum, ORVI, PwC) add and never subtract; they ignore opportunity cost and, per JLARC's own note, exclude externalities such as carbon and health costs. Brookings is the only model that measures a causal counterfactual, which is why it runs lowest and is the most defensible in a hearing.

## Construction coefficient anchors

| Project | Capacity | Construction jobs | Implied jobs/MW |
|---|---|---|---|
| Bedington, WV (Penzance) | ~600 MW | 1,000+ | ~1.7 |
| CoreWeave, Lancaster PA | ~300 MW | 600 | ~2.0 |
| Stargate, Michigan | ~1,000 MW | 2,500+ | ~2.5 |
| Meta, El Paso TX | ~1,000 MW | 4,000+ (peak) | ~4.0 |
| Meta, Sturgeon County AB | ~1,000 MW | ~3,000 (peak) | ~3.0 |
| AI campus, Pecos TX | ~2,000 MW | 6,000+ (peak) | ~3.0 |
| Meta Hyperion, Richland Parish LA | ~5,000 MW | ~7,500 (peak), build to ~2036 | ~1.5 |

## Key sources

- JLARC, "Data Centers in Virginia" (Report 598), December 2024. Per-facility staffing, 68% equipment capital split, five-year replacement cycle, statewide impact totals, IMPLAN externalities caveat.
- Brookings, "New evidence on data center employment effects" (Bahar and Wright), May 2026.
- Mangum Economics, Virginia data center impact analysis, 2023.
- Ohio River Valley Institute, data center economic development analysis, 2026.
- PwC for the Data Center Coalition, 2023, 2025 and 2026 impact studies (2026: 1,005,080 direct jobs in 2024; >4.5 other jobs per direct job nationally).
- Bahar and Wright, "The Local Economic Impact of Data Centers" (2026 working paper): county private employment +4-5% over 5-6 years (~2,000-4,000 jobs in a ~100,000-job county), wages +3-4%, IT gains driven by hyperscalers, incentives ~62% of investment for colocation vs ~2% for hyperscale.
- Food & Water Watch, "Artificial Jobs" (January 2026): ~$54M investment per Virginia data center job vs ~$137,000 elsewhere.
- Uptime Institute, 16th Global Data Center Survey (July 2026): over half of operators struggle to fill positions.
- Virginia 2026 budget: $0.011/kWh data center electricity tax, July 1 2026 to June 30 2028, capped at $600M/yr statewide.
- Project announcements: Gateway, Bedington, CoreWeave, Stargate, Meta (2025-2026).

## Audience views

The public/hearing view hides the industry-funded PwC model and the internal caveats. It never inflates a number; every public figure is a strict subset of the internal view. The headline public figure combines permanent jobs with a conservative independent or government model.

## Usage

Open `model.html` in any browser, or serve via GitHub Pages (Settings > Pages > Source: main, root); `index.html` redirects to it. No build step, no dependencies. Coefficients are editable in the script block at the bottom of `model.html`.

- **Share a scenario:** every input is saved in the URL hash (for example `model.html#mw=1000&ftype=ai&aud=pub`). Use "Copy link to this scenario".
- **Print / save PDF:** hides the controls and prints the results with a scenario line at the top.
- **Spreadsheet:** `dc_jobs_model.xlsx` mirrors the calculator's coefficients.

## Added in v2.0 (September 2026)

- AI training campus facility type (~0.20 permanent jobs/MW).
- Build cost per MW input and **capital per permanent job** output, with Food & Water Watch and Hyperion benchmarks.
- Construction split into average, peak, **job-years** (average x build duration) and **local residents** (average x local share, a stated assumption).
- **Range strip** showing permanent + spillover under every model at once.
- PwC updated to the 2026 study (~4.5x) with an optional state multiplier; Brookings revision flagged.
- **County effect** check from Brookings (2-5% private employment lift, 3-4% wages), not additive to the tiers.
- **Fiscal** section: electricity use, electricity tax (Virginia preset), local property tax with abatement, and forgone sales tax (internal only).
- Anchor projects table in the tool, shareable URLs, print layout, and `index.html` redirect.

## Caveats

The square-foot-to-MW conversion (~3,500 sq ft/MW) is loose; the industry estimates by power, not floor area. The Tier 2 FTE figure and the construction local-share default (50%) are assumptions. Fiscal figures use a single effective property tax rate and should be calibrated to the county's levy. Model multipliers are simplified to per-direct-job factors for a quick on-screen comparison; the source studies use fuller input-output structures.
