# Experiments Summary

Most experiments use `m = 10` pigeons, `n = 7` holes, 500 steps, and `n = 30` repetitions with paired t-tests on matched seeds. Experiment 5 uses `m = 12`, `n = 8`.

| # | Name | Perturbation | Key Finding | Classification |
|---|------|--------------|-------------|----------------|
| 1 | Frozen Holes | Freeze 0-6 holes permanently | System reaches the theoretical optimum up to 3 frozen holes; beyond that, repeat failure approaches 1.0 and capacity limits dominate | Tolerance + Structural Constraint |
| 2 | Policy Comparison | Replace all pigeons with GREEDY, EXPLORATORY, REPULSIVE, or COOPERATIVE | All policies achieve identical overload, but failed placements vary by 5x and same-target retry ranges from 0.46 to 1.00 | Emergent Behavior |
| 3 | Noisy Perception | Add Gaussian noise (`sigma = 0.5-5.0`) to perceived loads | Monotonic degradation with no noise buffer; even `sigma = 0.5` raises overload 12.2% (`rho = +0.638`) | Structural Constraint |
| 4 | View Radius | Restrict visibility to `r = 1, 2, 3, 5, 7` | All radii reach minimum overload; wider radius only accelerates convergence (11.8 steps at `r = 1` vs 2.0 at `r = 7`) | Basin Geometry |
| 5 | Chimeric Policies | Split the population 50/50 between two policies | All mixed-policy pairs reach identical overload, but same-policy pigeons cluster above chance (`0.738-0.796`) | Emergent Behavior |
| 6 | Recovery | Freeze hole `0` at step `167`, optionally heal at step `333` | Complete recovery with no hysteresis; healing halves failed placements and slightly reduces retry persistence | Tolerance |
| 7 | Progressive vs Sudden Damage | Freeze 3 holes all at step `100` or one each at `100/200/300` | Both reach identical overload; gradual damage yields 26% fewer failed placements and lower repeat failure | Basin Geometry |
| 8 | Misleading Holes | Mark 0-6 holes as misleading (report load `0`) | Most damaging perturbation: a single misleading hole captures 36% of pigeons and 66% of overload while raising overload 25.6% | Structural Constraint + Bias Formation |

## Classification Key

| Category | Description | Experiments |
|----------|-------------|-------------|
| **Tolerance** | Endpoint remains optimal despite perturbation | 1 (0-3 frozen), 6 |
| **Structural Constraint** | Hard limits where compensation fails | 1 (4-6 frozen), 3, 8 |
| **Emergent Behavior** | Same endpoint emerges from qualitatively different local dynamics | 2, 5 |
| **Basin Geometry** | Same attractor reached through smoother or rougher trajectories | 4, 7 |
| **Bias Formation** | Faults induce stable substrate or population asymmetries | 8 |
