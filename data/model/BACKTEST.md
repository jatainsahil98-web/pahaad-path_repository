# Backtest against PWD road closures

Season 2026-06-26 to 2026-07-25: 23 days, 39 PWD reports, 74 closures matched to PahaadPath stretches (relaxed matching).

| Thresholds | Cut-off | POD | FAR | CSI | TSS | Brier |
|---|---|---|---|---|---|---|
| Caine 1980 (in use) | Caution | 11% | 79% | 8% | 0.07 | 0.09 |
| Caine 1980 (in use) | Avoid | 0% | 100% | 0% | -0.01 |  |
| Fitted, 20% level | Caution | 96% | 90% | 10% | 0.07 | 0.43 |
| Fitted, 20% level | Avoid | 58% | 90% | 10% | 0.06 |  |

TSS at Caution for Caine: 95% interval -0.01 to 0.13.
Median warning lead time (Caine, Caution or worse before the closure): 0 h over 74 closures with a time.

Fitted thresholds are not in use: they did not beat Caine on held-out days by more than the interval.

Ground truth: Uttarakhand PWD SRMD closure reports. PWD names roads, not points, so matches to stretches are approximate. Rain: ERA5 hourly from Open-Meteo, the same source the Proof tab replays.

Susceptibility class: TSS at Caution 0.06552569052569053 with the DEM slope class, 0.1466067716067716 with the GSI NLSM class; the engine uses the GSI class.

# Model v6: more than rain

Stretch-days 2026-06-26 to 2026-07-25, 74 PWD closures (relaxed match). Cut-offs flag the same share of ordinary days as the current engine.

| | Closures warned (Caution) | Precision (Caution) | TSS (Caution) | Closures warned (Avoid) | Precision (Avoid) |
|---|---|---|---|---|---|
| Current engine (Caine) | 11% | 21% | 0.07 | 0% | 0% |
| v6: rain + static | 15% | 18% | 0.08 | 15% | 18% |

Parameter groups, added one at a time on held-out folds (kept when TSS rises by 0.01 or more):

| Groups | TSS (Caution) | Precision (Caution) | Kept |
|---|---|---|---|
| rain + static | 0.08 | 18% | yes |
| rain + static + soil | 0.08 | 18% | no |
| rain + static + peak | 0.04 | 13% | no |
| rain + static + season | 0.07 | 18% | no |
| rain + static + cold | 0.07 | 17% | no |
| rain + static + quake | 0.08 | 18% | no |
| rain + static + gsi | 0.07 | 21% | no |

v6 is not used: its TSS 0.08 is not above the top of the current engine's 95% range (-0.01 to 0.13).
