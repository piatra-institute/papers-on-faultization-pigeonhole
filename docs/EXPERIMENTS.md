# Experiments Summary

All experiments use m=10 pigeons, n=7 holes, 500 steps, n=30 repetitions with paired t-tests on matched seeds.

| # | Name | Perturbation | Key Finding | Classification |
|---|------|-------------|-------------|----------------|
| 1 | Frozen Holes | Disable 0-6 holes permanently | System reaches theoretical optimum up to 3 frozen holes; degrades sharply beyond, with ratio dropping to 0.174 at 6 frozen | Tolerance + Structural Constraint |
| 2 | Policy Comparison | Swap all pigeons to GREEDY, EXPLORATORY, REPULSIVE, or COOPERATIVE | All policies achieve identical overload but differ 5x in failed placements (REPULSIVE best, EXPLORATORY worst) | Emergent Behavior |
| 3 | Noisy Perception | Gaussian noise (sigma 0.5-5.0) on reported hole loads | Monotonic degradation with no noise buffer; even sigma=0.5 raises overload 12.2% (rho=+0.638) | Structural Constraint |
| 4 | View Radius | Restrict pigeon visibility to radius 1-7 | All radii reach minimum overload; wider radius only accelerates convergence (11.8 steps at r=1 vs 2.0 at r=7) | Basin Geometry |
| 5 | Chimeric Policies | Split population 50/50 between two policies | All mixed-policy pairs reach theoretical minimum; heterogeneous agents self-organize as effectively as homogeneous ones | Emergent Behavior |
| 6 | Recovery | Freeze 3 holes at step 200, optionally heal at step 350 | Complete recovery with no hysteresis; healing halves the cumulative failed placements | Tolerance |
| 7 | Progressive vs Sudden | Freeze 3 holes all at once or one per 50 steps | Both reach identical overload; gradual damage produces 26% fewer failed placements, acting as stress inoculation | Basin Geometry |
| 8 | Misleading Holes | 1-4 holes report artificially low loads | Most damaging perturbation: single misleading hole raises overload 25.6%, plateauing at +47% for 4 misleading (rho=+0.417) | Structural Constraint |

## Classification Key

| Category | Description | Experiments |
|----------|-------------|-------------|
| **Tolerance** | System fully compensates; perturbation absorbed without lasting effect | 1 (0-3 frozen), 6 |
| **Structural Constraint** | Hard limit beyond which compensation fails | 1 (4-6 frozen), 3, 8 |
| **Emergent Behavior** | Identical outcomes arise from qualitatively different mechanisms | 2, 5 |
| **Basin Geometry** | Same attractor reached, but path properties (speed, disruption) differ | 4, 7 |
