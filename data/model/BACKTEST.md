# Backtest against PWD road closures

Season 2026-06-26 to 2026-09-23: 85 days, 159 PWD reports, 423 closures matched to PahaadPath stretches (relaxed matching).

| Thresholds | Cut-off | POD | FAR | CSI | TSS | Brier |
|---|---|---|---|---|---|---|
| Caine 1980 | Caution | 8% | 65% | 7% | 0.04 | 0.18 |
| Caine 1980 | Avoid | 1% | 70% | 1% | 0.00 |  |
| Fitted, 20% level (in use) | Caution | 93% | 75% | 24% | 0.09 | 0.41 |
| Fitted, 20% level (in use) | Avoid | 65% | 74% | 23% | 0.10 |  |

TSS at Caution for Caine: 95% interval -0.00 to 0.08.
Median warning lead time (Caine, Caution or worse before the closure): 0 h over 391 closures with a time.

Fitted thresholds are in use: they beat Caine on held-out days by more than the interval.

Ground truth: Uttarakhand PWD SRMD closure reports. PWD names roads, not points, so matches to stretches are approximate. Rain: ERA5 hourly from Open-Meteo, the same source the Proof tab replays.

Susceptibility class: TSS at Caution 0.035018345284819154 with the DEM slope class, 0.07423036693848509 with the GSI NLSM class; the engine uses the GSI class.

# Model v6: more than rain

Stretch-days 2026-06-26 to 2026-09-23, 423 PWD closures (relaxed match). Cut-offs flag the same share of ordinary days as the current engine.

| | Closures warned (Caution) | Precision (Caution) | TSS (Caution) | Closures warned (Avoid) | Precision (Avoid) |
|---|---|---|---|---|---|
| Current engine (Caine) | 8% | 35% | 0.04 | 1% | 30% |
| v6: rain + static + gsi | 47% | 76% | 0.43 | 10% | 83% |

Parameter groups, added one at a time on held-out folds (kept when TSS rises by 0.01 or more):

| Groups | TSS (Caution) | Precision (Caution) | Kept |
|---|---|---|---|
| rain + static | 0.21 | 63% | yes |
| rain + static + gsi | 0.43 | 76% | yes |
| rain + static + gsi + soil | 0.43 | 81% | no |
| rain + static + gsi + peak | 0.42 | 76% | no |
| rain + static + gsi + season | 0.43 | 75% | no |
| rain + static + gsi + cold | 0.43 | 77% | no |
| rain + static + gsi + quake | 0.42 | 73% | no |

v6 is past the season check (it is used only if it also passes the check on other years, INDEPENDENT.md): its TSS 0.43 is above the top of the current engine's 95% range (-0.00 to 0.08).
