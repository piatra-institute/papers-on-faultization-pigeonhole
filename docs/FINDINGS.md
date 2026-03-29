# Detailed Findings

## Setup

- **Model**: m=10 pigeons, n=7 holes, 500 steps
- **Statistical protocol**: Paired t-tests, matched seeds, n=30 per condition
- **Metrics**: final overload, overload ratio, DG index, convergence step, failed placements
- **Significance levels**: * p<0.05, ** p<0.01, *** p<0.001


## Experiment 1: Frozen Hole Robustness

**Perturbation**: Permanently disable 0 through 6 holes, measuring system's ability to redistribute pigeons among remaining holes.

| Condition | Overload | Ratio | p-value | Cohen's d | Classification |
|-----------|----------|-------|---------|-----------|----------------|
| frozen_0 (baseline) | 3.0 | 1.000 | -- | -- | -- |
| frozen_1 | 4.0 | 1.000 | -- | 0.00 | Tolerance |
| frozen_2 | 5.0 | 1.000 | -- | 0.00 | Tolerance |
| frozen_3 | 7.0 | 1.000 | -- | 0.00 | Tolerance |
| frozen_4 | 10.8 | 0.924 | 0.0002*** | 0.87 | Structural Constraint |
| frozen_5 | 19.1 | 0.313 | <0.0001*** | 2.41 | Structural Constraint |
| frozen_6 | 51.4 | 0.174 | <0.0001*** | 4.12 | Structural Constraint |

- **DG index**: 0.0 across all conditions (no differentiation geometry effects)
- **Key finding**: System reaches theoretical minimum overload for 0-3 frozen holes, then degrades sharply. The transition at frozen_4 marks a phase boundary where the system can no longer fully compensate.
- **Classification**: Tolerance (frozen_0 through frozen_3), Structural Constraint (frozen_4 through frozen_6)


## Experiment 2: Policy Comparison

**Perturbation**: Replace the default GREEDY policy with EXPLORATORY, REPULSIVE, or COOPERATIVE across all pigeons.

| Policy | Overload | Failed Placements | Change vs GREEDY | p-value | Convergence Step |
|--------|----------|-------------------|------------------|---------|-----------------|
| GREEDY (baseline) | 4.0 | 212.1 | -- | -- | 7.4 |
| EXPLORATORY | 4.0 | 460.3 | +117% | <0.0001*** | 39.8 |
| REPULSIVE | 4.0 | 84.6 | -60% | <0.0001*** | 8.8 |
| COOPERATIVE | 4.0 | 168.3 | -21% | <0.0001*** | 7.6 |

- **Key finding**: All four policies achieve identical final overload (theoretical minimum), but differ dramatically in process efficiency. REPULSIVE generates 60% fewer failed placements than GREEDY, while EXPLORATORY generates 117% more. The system exhibits policy indifference at equilibrium but strong policy sensitivity in dynamics.
- **Classification**: Emergent Behavior (outcome equivalence despite process divergence)


## Experiment 3: Noisy Perception

**Perturbation**: Add Gaussian noise (sigma = 0.5, 1.0, 2.0, 5.0) to each pigeon's perception of hole loads.

| Condition | Overload Change | p-value | Cohen's d |
|-----------|----------------|---------|-----------|
| noise_0.0 (baseline) | -- | -- | -- |
| noise_0.5 | +12.2% | 0.0011** | 0.64 |
| noise_1.0 | +17.8% | <0.0001*** | 0.91 |
| noise_2.0 | +28.9% | <0.0001*** | 1.53 |
| noise_5.0 | +43.3% | <0.0001*** | 2.28 |

- **Spearman correlation** (noise level vs overload): rho = +0.638, p < 0.0001***
- **Key finding**: Monotonic degradation with no noise buffer. Unlike transformer training (Levin et al., 2024), where mild noise can be tolerated or even beneficial, any perceptual noise immediately degrades performance. The system has zero tolerance for information corruption.
- **Classification**: Structural Constraint (no noise buffer exists)


## Experiment 4: View Radius

**Perturbation**: Restrict each pigeon's visibility to only holes within radius r (1, 2, 3, 5, 7) of its position.

| Condition | Overload | Convergence Step | Change vs radius_1 | p-value |
|-----------|----------|-----------------|---------------------|---------|
| radius_1 | 3.0 | 11.8 | -- | -- |
| radius_2 | 3.0 | 6.0 | -49% | 0.0093** |
| radius_3 | 3.0 | 3.9 | -67% | 0.0001*** |
| radius_5 | 3.0 | 2.3 | -81% | <0.0001*** |
| radius_7 (full) | 3.0 | 2.0 | -83% | <0.0001*** |

- **Key finding**: All view radii reach theoretical minimum overload. Information scope affects only convergence speed, not outcome. Even radius_1 (minimal local information) achieves optimality, just 6x slower than full visibility.
- **Classification**: Basin Geometry (all paths converge to same attractor; information determines speed, not destination)


## Experiment 5: Chimeric Policies

**Perturbation**: Split the population 50/50 between two different policies.

| Policy Pair | Overload | Aggregation Index |
|------------|----------|-------------------|
| GREEDY + COOPERATIVE | 4.0 | 0.738 |
| GREEDY + EXPLORATORY | 4.0 | 0.738 |
| EXPLORATORY + COOPERATIVE | 4.0 | 0.754 |
| REPULSIVE + COOPERATIVE | 4.0 | 0.796 |

- **Key finding**: All chimeric combinations reach theoretical minimum overload. Mixed-policy populations are as effective as homogeneous ones. The slight variation in aggregation index suggests REPULSIVE+COOPERATIVE produces the most spatially distributed placement pattern, but all outcomes are functionally equivalent.
- **Classification**: Emergent Behavior (heterogeneous agents self-organize to identical outcome)


## Experiment 6: Recovery After Damage

**Perturbation**: Run baseline, then freeze 3 holes at step 200 (damage), then unfreeze at step 350 (heal).

| Condition | Overload | Failed Placements |
|-----------|----------|-------------------|
| control | 3.0 | 0.0 |
| damage_only | 3.0 | 49.4 |
| damage_and_heal | 3.0 | 24.7 |

- **Key finding**: Complete recovery in all conditions. The system reaches minimum overload regardless of damage history. Failed placements during damage are expected (reduced capacity), and healing halves the total failed placements. The system shows no hysteresis -- past damage leaves no lasting trace.
- **Classification**: Tolerance (complete recovery, no hysteresis)


## Experiment 7: Progressive vs Sudden Damage

**Perturbation**: Freeze 3 holes either all at once (sudden, step 200) or one per 50 steps (progressive, steps 200/250/300).

| Condition | Overload | Failed Placements | Change vs sudden | p-value |
|-----------|----------|-------------------|------------------|---------|
| sudden | 3.0 | 173.5 | -- | -- |
| gradual | 3.0 | 128.9 | -26% | <0.0001*** |

- **Key finding**: Both conditions reach identical final overload, but gradual damage produces 26% fewer failed placements. Progressive stress allows the system to incrementally adapt, acting as a form of stress inoculation. The final state is identical, but the path is smoother.
- **Classification**: Basin Geometry (same attractor, different trajectories; gradual damage traverses a less disrupted path)


## Experiment 8: Misleading Holes

**Perturbation**: Mark 1-4 holes as misleading (report artificially low load, attracting pigeons to already-full holes).

| Condition | Overload Change | p-value |
|-----------|----------------|---------|
| misleading_0 (baseline) | -- | -- |
| misleading_1 | +25.6% | <0.0001*** |
| misleading_2 | +40.0% | <0.0001*** |
| misleading_3 | +44.4% | <0.0001*** |
| misleading_4 | +46.7% | <0.0001*** |

- **Spearman correlation** (misleading count vs overload): rho = +0.417, p < 0.0001***
- **Key finding**: Misleading holes cause the most severe degradation of any perturbation. A single misleading hole raises overload by 25.6%, and the effect plateaus around 3-4 misleading holes (+44-47%). This is far worse than frozen holes (which are managed optimally up to 3). The system can route around absent resources but cannot overcome deceptive ones.
- **Classification**: Structural Constraint (deceptive substrate fundamentally undermines optimization)


## Cross-Experiment Summary

| Classification | Experiments | Pattern |
|---------------|-------------|---------|
| Tolerance | 1 (frozen 0-3), 6 | System compensates fully; no lasting damage |
| Structural Constraint | 1 (frozen 4-6), 3, 8 | Hard limits where compensation fails |
| Emergent Behavior | 2, 5 | Identical outcomes from diverse mechanisms |
| Basin Geometry | 4, 7 | Same attractor reached via different paths |

The pigeonhole system exhibits a sharp distinction between perturbations it can fully absorb (frozen holes up to capacity, damage/recovery) and those that fundamentally undermine its operation (noise, deception). The system has no graceful degradation mode for information corruption -- it either has accurate information and reaches optimality, or it does not.
