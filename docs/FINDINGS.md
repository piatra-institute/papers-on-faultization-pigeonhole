# Detailed Findings

## Setup

- **Base model**: `m = 10`, `n = 7`, 500 steps, asynchronous activation
- **Exception**: Experiment 5 uses `m = 12`, `n = 8`
- **Statistical protocol**: paired t-tests with matched seeds, `n = 30` per condition
- **Primary metrics**: final overload, overload ratio, convergence step, failed placements
- **Learning-like metrics**: post-failure same-target retry, post-failure repeat-failure rate
- **Bias metrics**: misleading-hole occupancy share/bias, misleading-hole overload share/bias, misleading load gap
- **Negative result retained**: DG index is `0.0` in all conditions


## Experiment 1: Frozen Hole Robustness

**Perturbation**: Permanently freeze 0 through 6 holes.

| Condition | Overload | Ratio | Same-Target Retry | Repeat Failure | Classification |
|-----------|----------|-------|-------------------|----------------|----------------|
| frozen_0 | 3.00 | 1.000 | 0.000 | 0.000 | -- |
| frozen_1 | 4.00 | 1.000 | 0.542 | 0.542 | Tolerance |
| frozen_2 | 5.00 | 1.000 | 0.486 | 0.985 | Tolerance |
| frozen_3 | 6.00 | 1.000 | 0.309 | 0.929 | Tolerance |
| frozen_4 | 6.47 | 0.924 | 0.247 | 0.985 | Structural Constraint |
| frozen_5 | 2.50 | 0.313 | 0.198 | 1.000 | Structural Constraint |
| frozen_6 | 1.57 | 0.174 | 0.162 | 1.000 | Structural Constraint |

- **Key finding**: The system reaches the theoretical minimum overload for 0-3 frozen holes, then degrades sharply at frozen_4 and beyond.
- **Learning-like finding**: There is little evidence of negative learning from rejection. When only one hole is frozen, pigeons retry the same faulty target on their next attempted move 54% of the time. With multiple frozen holes, repeat failure approaches 100%, meaning agents keep colliding with damaged substrate rather than learning to avoid it.
- **Classification**: Tolerance (frozen_0 through frozen_3), Structural Constraint (frozen_4 through frozen_6)


## Experiment 2: Policy Comparison

**Perturbation**: Replace the default policy with GREEDY, EXPLORATORY, REPULSIVE, or COOPERATIVE under `1` frozen hole.

| Policy | Overload | Failed Placements | Same-Target Retry | Repeat Failure | Convergence Step |
|--------|----------|-------------------|-------------------|----------------|-----------------|
| GREEDY | 4.0 | 212.1 | 0.542 | 0.542 | 7.4 |
| EXPLORATORY | 4.0 | 460.3 | 0.940 | 0.940 | 39.8 |
| REPULSIVE | 4.0 | 84.6 | 0.463 | 0.463 | 8.8 |
| COOPERATIVE | 4.0 | 168.3 | 0.997 | 0.997 | 7.6 |

- **Key finding**: All four policies reach identical final overload, but process cost diverges sharply. Failed placements vary by more than 5x, and post-failure persistence varies even more.
- **Learning-like finding**: The strongest evidence against agent-level learning appears here. After rejection, EXPLORATORY retries the same frozen hole 94% of the time and COOPERATIVE nearly 100% of the time. REPULSIVE is the least persistent, but still retries 46% of the time.
- **Classification**: Emergent Behavior. Outcome equivalence coexists with sharp differences in fault susceptibility and retry persistence.


## Experiment 3: Noisy Perception

**Perturbation**: Add Gaussian noise (`sigma = 0.5, 1.0, 2.0, 5.0`) to perceived hole loads.

| Condition | Overload Change | p-value | Cohen's d |
|-----------|----------------|---------|-----------|
| noise_0.0 | -- | -- | -- |
| noise_0.5 | +12.2% | 0.0011** | 0.66 |
| noise_1.0 | +17.8% | <0.0001*** | 1.05 |
| noise_2.0 | +28.9% | <0.0001*** | 1.38 |
| noise_5.0 | +43.3% | <0.0001*** | 1.85 |

- **Spearman correlation** (noise vs overload): `rho = +0.638`, `p < 0.0001`
- **Key finding**: Monotonic degradation with no noise buffer. Any information corruption immediately worsens allocation quality.
- **Classification**: Structural Constraint


## Experiment 4: View Radius

**Perturbation**: Restrict visibility to radius `r in {1, 2, 3, 5, 7}`.

| Radius | Overload | Convergence Step | Change vs radius_1 | p-value |
|--------|----------|------------------|--------------------|---------|
| 1 | 3.0 | 11.8 | -- | -- |
| 2 | 3.0 | 6.0 | -49% | 0.0093** |
| 3 | 3.0 | 3.9 | -67% | 0.0001*** |
| 5 | 3.0 | 2.3 | -81% | <0.0001*** |
| 7 | 3.0 | 2.0 | -83% | <0.0001*** |

- **Key finding**: Information scope affects speed, not destination. Even radius_1 reaches the optimum.
- **Classification**: Basin Geometry


## Experiment 5: Chimeric Policies

**Perturbation**: Split the population 50/50 between two policies (`m = 12`, `n = 8`).

| Policy Pair | Overload | Aggregation Index |
|------------|----------|-------------------|
| GREEDY + COOPERATIVE | 4.0 | 0.738 |
| GREEDY + EXPLORATORY | 4.0 | 0.738 |
| EXPLORATORY + COOPERATIVE | 4.0 | 0.754 |
| REPULSIVE + COOPERATIVE | 4.0 | 0.796 |

- **Key finding**: Mixed-policy populations are as effective as homogeneous ones, but they self-segregate above chance by policy type.
- **Classification**: Emergent Behavior


## Experiment 6: Recovery After Damage

**Perturbation**: Freeze hole `0` at step `167`, optionally heal it at step `333`.

| Condition | Overload | Failed Placements | Same-Target Retry | Repeat Failure |
|-----------|----------|-------------------|-------------------|----------------|
| control | 3.0 | 0.0 | 0.000 | 0.000 |
| damage_only | 3.0 | 49.4 | 0.257 | 0.257 |
| damage_and_heal | 3.0 | 24.7 | 0.226 | 0.211 |

- **Key finding**: Final overload is unchanged by damage history, and healing halves wasted actions.
- **Learning-like finding**: Post-failure persistence is much lower here than in the static frozen-hole experiments, but still not zero. The system reorganizes around damage, yet individual pigeons still show some retry persistence instead of explicit avoidance memory.
- **Classification**: Tolerance. Complete recovery with no hysteresis at the outcome level.


## Experiment 7: Progressive vs Sudden Damage

**Perturbation**: Freeze 3 holes either all at step `100` (sudden) or one each at steps `100`, `200`, and `300` (gradual).

| Condition | Overload | Failed Placements | Same-Target Retry | Repeat Failure |
|-----------|----------|-------------------|-------------------|----------------|
| sudden | 3.0 | 173.5 | 0.249 | 0.744 |
| gradual | 3.0 | 128.9 | 0.253 | 0.639 |

- **Key finding**: The endpoint is identical, but gradual damage produces 26% fewer failed placements.
- **Learning-like finding**: Same-target retry is unchanged, but repeat failure is significantly lower under gradual damage. The system’s path gets smoother without acquiring actual memory.
- **Classification**: Basin Geometry. Temporal profile changes disruption cost, not the attractor.


## Experiment 8: Misleading Holes

**Perturbation**: Mark 0-6 holes as misleading. Misleading holes still accept pigeons but always report load `0`.

| Condition | Overload Change | Occupancy Bias | Overload Bias | Load Gap |
|-----------|----------------|----------------|---------------|----------|
| misleading_1 | +25.6% | +0.217 | +0.518 | +2.533 |
| misleading_2 | +40.0% | +0.274 | +0.559 | +1.920 |
| misleading_3 | +44.4% | +0.265 | +0.511 | +1.544 |
| misleading_4 | +46.7% | +0.219 | +0.418 | +1.275 |
| misleading_5 | +45.6% | +0.156 | +0.286 | +1.090 |
| misleading_6 | +43.3% | +0.080 | +0.143 | +0.928 |

- **Spearman correlation** (misleading count vs overload): `rho = +0.417`, `p < 0.0001`
- **Bias finding**: A single misleading hole occupies just 14% of the substrate but captures 36% of pigeons and 66% of overload. With two misleading holes, deceptive substrate captures 56% of pigeons and 85% of overload.
- **Key finding**: Misleading holes do not just increase overload; they induce a strong attraction bias that concentrates both occupancy and excess load on deceptive substrate.
- **Classification**: Structural Constraint with strong fault-induced bias formation.


## Cross-Experiment Summary

| Pattern | Experiments | Interpretation |
|---------|-------------|----------------|
| Outcome tolerance | 1 (frozen 0-3), 6 | The system compensates fully at the endpoint |
| Process divergence | 2, 7 | Same endpoint, sharply different wasted-action profiles |
| Fault persistence | 1, 2, 6, 7 | Rejected pigeons often retry faulty substrate instead of learning to avoid it |
| Bias formation | 5, 8 | Faults and policy mixtures induce stable asymmetries not present in the nominal specification |
| Structural constraint | 1 (frozen 4-6), 3, 8 | Hard perturbation regimes where compensation fails |

The updated picture is more specific than “DG is absent.” This system is strongly adaptive at the collective level, but it does not show convincing agent-level learning. Instead, faultization reveals persistent retry dynamics under rejection and strong load-attraction bias under deception.
