# Why the NFL Ended the Pro Bowl Games: Viewership Analytics Project

Analysis of why the NFL discontinued its all-star event (flag football game and skills events) in 2026.

## Contents
- `pro_bowl_viewership.csv` : annual average audience, 2022-2026, plus format, day, network, venue, and model columns
- Research paper (Claude Doc): abstract, method, results, discussion, limitations, references
- Dashboard page: charts, trend model, and diagrams

## Data dictionary
| Column | Meaning |
|---|---|
| year | Event year |
| format | Tackle game or Pro Bowl Games |
| day / network / venue | Broadcast context |
| avg_viewers_millions | Reported average TV audience |
| yoy_pct | Year-over-year change, computed from the rounded figures |
| trend_fit_millions | OLS fit (2022-2025 only), extrapolated to 2026 |
| residual_millions | Actual minus fit |

## Method
1. Compile reported audiences from trade press.
2. Fit `viewers = 6.85 - 0.65 * (year - 2022)` on 2022-2025 (R^2 ~0.94, n = 4).
3. Extrapolate to 2026 (4.25M) and compare with the observed ~1.92M.
4. Split the total 2022-2026 decline (4.8M) into trend (~2.45M, 51%) and residual shock (~2.3M, 49%).

## Findings
- Viewership fell ~70% over four years and ~60% in the final year.
- About half the decline followed the existing trend; half came with the 2026 changes (Tuesday, ESPN only, indoor venue).
- Day, network, venue, and player pool all changed at once, so the 2026 shock cannot be attributed to one cause.

## Caveats
Five rounded data points from trade-press reports, not a single measurement source. The trend model is descriptive, not causal. Verify venue and network details before citing. The skills competition was never reported separately.

## Reproduce
```python
import numpy as np
t = np.arange(4); y = np.array([6.7, 6.3, 5.8, 4.7])
slope, intercept = np.polyfit(t, y, 1)   # -0.65, 6.85
print(intercept + slope * 4)             # 4.25 predicted for 2026
```

## Sources
Front Office Sports, Awful Announcing, Sports Media Watch (2026 coverage).
