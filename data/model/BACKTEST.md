# Backtest against PWD road closures

Season 2026-06-26 to 2026-09-03: 55 days, 99 PWD reports, 275 closures matched to PahaadPath stretches (relaxed matching).

| Thresholds | Cut-off | POD | FAR | CSI | TSS | Brier |
|---|---|---|---|---|---|---|
| Caine 1980 (in use) | Caution | 11% | 66% | 9% | 0.06 | 0.16 |
| Caine 1980 (in use) | Avoid | 1% | 70% | 1% | 0.00 |  |
| Fitted, 10% level | Caution | 98% | 78% | 21% | 0.05 | 0.44 |
| Fitted, 10% level | Avoid | 64% | 78% | 20% | 0.05 |  |

TSS at Caution for Caine: 95% interval -0.01 to 0.12.
Median warning lead time (Caine, Caution or worse before the closure): 0 h over 243 closures with a time.

Fitted thresholds are not in use: they did not beat Caine on held-out days by more than the interval.

Ground truth: Uttarakhand PWD SRMD closure reports. PWD names roads, not points, so matches to stretches are approximate. Rain: ERA5 hourly from Open-Meteo, the same source the Proof tab replays.

Susceptibility class: TSS at Caution 0.0551257618679715 with the DEM slope class, 0.11155979053996051 with the GSI NLSM class; the engine uses the GSI class.

# Model v6: more than rain

Stretch-days 2026-06-26 to 2026-09-03, 275 PWD closures (relaxed match). Cut-offs flag the same share of ordinary days as the current engine.

| | Closures warned (Caution) | Precision (Caution) | TSS (Caution) | Closures warned (Avoid) | Precision (Avoid) |
|---|---|---|---|---|---|
| Current engine (Caine) | 11% | 34% | 0.06 | 1% | 30% |
| v6: rain + static + gsi + soil + peak | 49% | 79% | 0.46 | 25% | 80% |

Parameter groups, added one at a time on held-out folds (kept when TSS rises by 0.01 or more):

| Groups | TSS (Caution) | Precision (Caution) | Kept |
|---|---|---|---|
| rain + static | 0.30 | 74% | yes |
| rain + static + gsi | 0.41 | 77% | yes |
| rain + static + gsi + soil | 0.45 | 77% | yes |
| rain + static + gsi + soil + peak | 0.46 | 79% | yes |
| rain + static + gsi + soil + peak + quake | 0.46 | 80% | no |
| rain + static + gsi + soil + peak + season | 0.41 | 82% | no |
| rain + static + gsi + soil + peak + cold | 0.46 | 79% | no |

v6 is past the season check (it is used only if it also passes the check on other years, INDEPENDENT.md): its TSS 0.46 is above the top of the current engine's 95% range (-0.01 to 0.12).
