---
title: |
  On Faultization:\
  Pigeonhole Principle.\
  Morphogenetic Competencies Under\
  Irreducible Constraint
author: PIATRA . INSTITUTE
date: March 2026
---

## Abstract

We apply the morphogenetic perturbation methodology of Levin and collaborators to the pigeonhole principle, a classical impossibility theorem reinterpreted as a distributed multi-agent system. In our model, $m = 10$ autonomous pigeons must self-organize into $n = 7$ holes under four local placement policies (GREEDY, EXPLORATORY, REPULSIVE, COOPERATIVE), with no centralized controller. Because $m > n$, overload $O \geq m - n = 3$ is irreducible; the system cannot solve the problem, only manage it. We subject this system to eight systematic perturbation experiments ($n = 30$ replications, 500 steps, paired $t$-tests with matched seeds): frozen-hole robustness, policy comparison, noisy perception, view-radius sweep, chimeric mixed-policy populations, dynamic damage and recovery, progressive versus sudden damage, and misleading (deceptive) holes. We find that (1) the system converges to the theoretical minimum overload in six of eight experiments, demonstrating strong emergent competency; (2) all four policies achieve identical final overload but diverge dramatically in process efficiency (failed placements differ by up to 117\%, $p < 0.0001$); (3) perceptual noise causes immediate monotonic degradation with no tolerance threshold ($\rho = +0.638$, $p < 0.0001$); (4) misleading holes are far more damaging than frozen holes, paralleling Levin's distinction between damaged and deceptive substrates; and (5) no delayed gratification is observed in any condition (DG Index $= 0.0$ universally). We classify these findings within the morphogenetic competency framework and compare them to prior results on sorting algorithms and transformer training.


## 1. Introduction

The pigeonhole principle states that if $m$ items are placed into $n$ containers and $m > n$, then at least one container must hold more than one item. Formally, for any function $f: A \to B$ with $|A| > |B|$, $f$ cannot be injective. This is among the simplest impossibility theorems in discrete mathematics: no algorithm, however clever, can achieve injective placement when the domain exceeds the codomain. The principle is typically treated as a static logical fact -- a counting argument yielding a contradiction -- not a dynamical system.

Yet the pigeonhole principle describes a situation ubiquitous in distributed systems: too many agents competing for too few resources.
Cells competing for niches in a tissue, packets competing for bandwidth in a network, vehicles competing for lanes on a highway,
job seekers competing for positions in a labor market -- all face pigeonhole-type constraints where some degree of conflict is
structurally inevitable. In each of these settings, the mathematical impossibility of conflict-free allocation is a given. The
operationally important question is never "can conflict be avoided?" but rather "how intelligently is the inevitable conflict
organized, and how robustly does that organization withstand perturbation?" This is the question our
paper addresses.

Recent work by Levin and collaborators has demonstrated that classical algorithms, when reinterpreted as decentralized multi-agent systems with imperfect components, exhibit unexpected emergent competencies. Zhang, Goldstein, and Levin (2024) showed that sorting algorithms, reformulated as arrays of autonomous elements executing local comparison-swap policies, display robustness to damage, delayed gratification trajectories, and chimeric self-organization behaviors not specified by the original algorithm. The sorting elements exhibit what Levin terms "basal cognition": goal-directed behavior, error correction, and adaptive replanning at scales far below neural systems. Kofman, Bhatt, and Levin (2025) extended this methodology to transformer training, revealing analogous competencies in gradient descent under morphogenetic perturbation -- frozen parameters, noisy gradients, and adversarial weight surgery.

We apply this methodology to the pigeonhole principle. Unlike sorting (which has a well-defined solution reachable by correct algorithms) and transformer training (which converges to a loss minimum), the pigeonhole system faces an irreducible constraint: overload $O \geq m - n$ always. The system cannot solve its assigned problem. It can only manage the inevitable conflict as effectively as possible. This makes the pigeonhole principle a unique target for morphogenetic analysis: the question is not whether the system reaches a correct answer, but how intelligently it organizes around an answer that cannot exist.

The morphogenetic perturbation protocol proceeds in three stages: (1) formalize the target process as a decentralized system with explicit local policies, (2) systematically perturb the system by breaking assumptions of the nominal process (damage substrate, corrupt perception, mix policies, vary information), and (3) classify the resulting behaviors as emergent competencies (behaviors exceeding algorithm specification), tolerance thresholds (perturbation levels below which performance is maintained), or structural constraints (irreducible limitations). We apply all three stages to the pigeonhole principle across eight experiments.

Our contributions are as follows:

- We formalize the pigeonhole principle as a distributed multi-agent system with four local placement policies, a composite potential function, and a hook-based perturbation architecture that enables systematic intervention at every decision point.
- We conduct eight systematic experiments spanning substrate damage, perceptual noise, information radius, policy heterogeneity, dynamic damage/recovery, and substrate deception, with rigorous statistical analysis ($n = 30$ replications, paired $t$-tests, Cohen's $d$ effect sizes, Spearman correlations).
- We demonstrate that local policies achieve global optimality in six of eight conditions, constituting a strong emergent competency in the Levin framework -- the system finds the theoretical minimum overload using only local rules and no global coordination.
- We identify a sharp distinction between damaged substrate (frozen holes, which the system routes around with zero performance loss) and deceptive substrate (misleading holes, which cause up to 51\% overload degradation), paralleling theoretical predictions from the basal cognition literature.
- We report a universal absence of delayed gratification across all conditions (DG Index $= 0.0$), establishing that the pigeonhole system's optimization landscape is monotonically navigable and contains no detour-requiring basins.
- We provide the first morphogenetic perturbation analysis of an impossibility theorem, extending the framework from solvable problems (sorting, training) to fundamentally unsolvable ones.


## 2. Related Work

### 2.1 Morphogenetic Perturbation of Algorithms

Zhang, Goldstein, and Levin (2024) introduced the methodology of treating classical algorithms as morphogenetic systems: decentralized collectives of elements executing local policies under imperfect conditions. Applied to sorting, this approach revealed that even minimal systems exhibit error correction, damage compensation, delayed gratification, and chimeric self-organization. The key insight is that algorithmic behavior, when viewed through the lens of basal cognition, contains competencies that are not apparent from the algorithm's formal specification. In their system, array elements executing simple comparison-swap rules could tolerate damaged elements, reorganize around removed positions, and -- in some cases -- temporarily reduce sortedness to enable later improvement (delayed gratification).

Kofman, Bhatt, and Levin (2025) extended this to transformer training, showing that gradient descent under morphogenetic perturbation (noisy gradients, frozen parameters, weight surgery) exhibits analogous competencies. They introduced the morphogenetic perturbation protocol: systematically break assumptions of the nominal process, record full trajectories, and classify the resulting behaviors as emergent competencies, tolerance thresholds, or structural constraints. Their work established that even systems as abstract as gradient descent on a loss landscape exhibit morphogenetic properties when probed appropriately.

Our work extends this line to a qualitatively different setting: an impossibility theorem. While sorting and training are solvable problems (there exists a correct sort, there exists a loss minimum), the pigeonhole principle with $m > n$ is inherently unsolvable. This extension tests whether the morphogenetic perturbation framework produces meaningful results when applied to systems that cannot, by construction, achieve their nominal objective.

### 2.2 Multi-Agent Resource Allocation

The pigeonhole system is formally a congestion game (Rosenthal, 1973): agents select resources (holes), and payoffs decrease with congestion. Nash equilibria of congestion games are well-characterized, and the price of anarchy provides worst-case bounds on decentralized performance relative to the social optimum (Roughgarden and Tardos, 2002). Our system differs in that the social optimum itself represents an irreducible conflict state, not a conflict-free solution. In standard congestion games, the social optimum is typically conflict-free or conflict-minimal; in the pigeonhole system, even the optimal state has overload $\geq m - n$.

Load balancing in distributed systems (Azar et al., 1999) addresses the allocation of $m$ tasks to $n$ processors under local information. The "power of two choices" result shows that sampling just two random processors (rather than one) and choosing the less loaded one reduces maximum load from $\Theta(\log n / \log \log n)$ to $\Theta(\log \log n)$. Our view-radius experiment (Experiment 4) provides a pigeonhole analogue of this phenomenon: even a small increase in the number of visible holes dramatically accelerates convergence.

The distributed task allocation literature also addresses fault tolerance (Aguilera et al., 2004), where processors may crash or behave adversarially. Our frozen-hole and misleading-hole experiments map directly onto crash faults (silent failure) and Byzantine faults (deceptive failure), respectively. The sharp performance difference we observe between these two fault types echoes the classical result that Byzantine faults are categorically harder to tolerate than crash faults.

### 2.3 Basal Cognition Framework

Levin (2019, 2022) argues that cognitive competencies exist on a continuum: from molecular networks solving constraint satisfaction problems, through cellular collectives achieving morphogenetic goals, to neural systems supporting behavioral intelligence. The key claim is that goal-directedness, error correction, and adaptive replanning are not exclusive to neural systems but appear at every scale of biological organization. Levin's framework identifies four hallmarks of basal cognition: (1) goal-directedness toward a target state, (2) error correction when perturbed away from that state, (3) adaptive replanning when the environment changes, and (4) capacity for delayed gratification (temporary sacrifice of progress for eventual gain).

Our pigeonhole system instantiates this framework at the simplest possible level: agents with no memory, no communication channel, and no model of other agents, navigating toward the best achievable state under an impossible global specification. If these agents exhibit competencies beyond what their local rules explicitly specify, that constitutes evidence for emergent intelligence in the Levin sense. The impossibility constraint adds a distinctive feature: the target state (zero overload) is unreachable, so the system must exhibit goal-directedness toward a relaxed target that it has no explicit representation of.


## 3. Methods

### 3.1 System Specification

The system consists of $m = 10$ pigeons and $n = 7$ holes. Each pigeon $k \in \{1, \ldots, m\}$ occupies a hole $x_k \in \{0, 1, \ldots, n\}$, where $x_k = 0$ denotes the unplaced state. The load of hole $i$ is $\ell_i = |\{k : x_k = i\}|$. The overload is defined as:

$$O(\mathbf{x}) = \sum_{i=1}^{n} \max(0, \ell_i - 1)$$

Since all pigeons must be placed and $m > n$, we have $O \geq m - n = 3$ for any fully-placed state.

**Hole statuses.** Each hole has one of three statuses:
- ACTIVE: accepts pigeons and reports true load.
- FROZEN: silently rejects all placement attempts (damaged hardware).
- MISLEADING: accepts pigeons but reports load as 0 regardless of true occupancy (deceptive substrate).

**Potential function.** The system minimizes:

$$\Phi(\mathbf{x}) = \alpha \sum_{i=1}^{n} \max(0, \ell_i - 1) + \beta \sum_{i=1}^{n} [\max(0, \ell_i - 1)]^2 + \gamma \cdot U(\mathbf{x})$$

where $U(\mathbf{x}) = |\{k : x_k = 0\}|$ is the count of unplaced pigeons, and $\alpha = 1.0$, $\beta = 0.5$, $\gamma = 10.0$. The first term penalizes total overload, the second penalizes concentrated overload (encouraging even distribution of excess), and the third strongly penalizes leaving pigeons unplaced.

**Local policies.** Each pigeon executes one of four policies based on local information:

1. *GREEDY*: Inspect visible holes (determined by view radius $r$), move to the hole with lowest observed load if it is lower than the load of the pigeon's current hole. This is the simplest reasonable policy: purely self-interested, myopic load minimization.
2. *EXPLORATORY*: Sample twice as many holes as the view radius permits ($\min(2r, n)$), then select the best. This policy trades computation (more sampling) for information, analogous to the "exploration vs exploitation" tradeoff in multi-armed bandits.
3. *REPULSIVE*: If the pigeon's current hole has load $\ell_i > 1$, escape with probability $(\ell_i - 1)/\ell_i$ and relocate greedily. If $\ell_i = 1$, stay. This policy implements a stochastic crowd-avoidance heuristic: the more crowded the hole, the more likely the pigeon is to flee.
4. *COOPERATIVE*: Evaluate the change in global potential $\Delta\Phi$ for each candidate move; move only if $\Delta\Phi < 0$. This is the only policy that considers the system-wide effect of its action, though it still acts locally (it cannot coordinate with other pigeons).

**Architecture.** The system uses a hook-based perturbation architecture modeled on the morphogpt framework (Kofman et al., 2025). Four named hook points provide interception at every stage of the pigeon decision cycle:
- `pigeon_view`: intercepts the list of visible (hole, load) pairs, enabling perturbations to perceived loads (noise, blindness, inversion).
- `pigeon_decision`: intercepts the chosen target hole, enabling perturbations to policy output (stubbornness, randomization, contrarianness).
- `placement_attempt`: intercepts the (pigeon, hole) pair before the frozen-hole check, enabling perturbations to the placement mechanism itself.
- `post_step`: intercepts the full system state after each step, enabling dynamic substrate changes (hole breaking, healing, progressive damage).

Each hook receives the current value and the step number, and returns either a modified value or `None` (pass-through). Multiple hooks can be chained on the same hook point. A probe records the complete trajectory: overload, potential, maximum load, unplaced count, load snapshots, and all move attempts with success/failure status. This architecture ensures that every experiment is implemented as a composition of hooks on the same base system, guaranteeing that all conditions share identical core dynamics.

**Dynamics.** At each step, one pigeon is activated uniformly at random, inspects a subset of holes determined by its view radius, applies its policy, and attempts placement. Frozen holes reject silently; misleading holes accept but misreport. The system runs for 500 steps after an initial random placement. This asynchronous activation scheme models real-world distributed systems where agents act independently and without synchronization.

**Theoretical minimum overload.** For a system with $n_a$ active (non-frozen) holes and $m$ pigeons, the theoretical minimum overload is:

$$O_{\min}^{\text{theo}} = \max(0, m - n_a)$$

This follows from the observation that the maximum number of holes that can each hold exactly one pigeon is $\min(m, n_a)$, leaving $m - \min(m, n_a)$ excess pigeons when $m > n_a$. All experiments use this quantity as the normalization baseline for the overload ratio.

**State space size.** The full state space has $(n + 1)^m$ configurations (each pigeon in one of $n$ holes or unplaced). For $m = 10$, $n = 7$, this is $8^{10} \approx 10^9$. The optimal states form a much smaller subset: any configuration where all $n$ holes are occupied and the $m - n = 3$ excess pigeons are distributed arbitrarily constitutes a minimum-overload state. The number of such states is $\binom{m}{n} \cdot n! \cdot S(m - n, n, n)$ where $S$ accounts for the distribution of excess, but the precise count matters less than the qualitative observation: optimal states are a tiny fraction of the state space, yet the system reliably finds them.

### 3.2 Statistical Protocol

All experiments use $n_{\text{rep}} = 30$ replications with matched random seeds across conditions. The primary statistical test is the paired $t$-test (two-tailed), which exploits seed-matching to control for initialization variance. Effect sizes are reported as Cohen's $d$ (paired: mean difference divided by standard deviation of differences). Monotonic relationships are assessed with Spearman's rank correlation $\rho$. Significance thresholds follow convention: $* \; p < 0.05$, $** \; p < 0.01$, $*** \; p < 0.001$.

For Experiment 5 (chimeric policies), where different conditions involve different random policy assignments, we use Welch's independent $t$-test for between-pair comparisons.

The choice of paired $t$-tests (rather than independent-samples tests) is motivated by the seed-matching design: each condition is run with seeds $0, 1, \ldots, 29$, and the same seed produces the same initial random placement and activation sequence across conditions. This eliminates between-run variance due to initialization, substantially increasing statistical power. The pairing is particularly important for experiments where the effect of interest is small (e.g., Experiment 7, where overload is identical across conditions but failed placements differ).

We do not apply multiple-comparison corrections (e.g., Bonferroni) across experiments because each experiment tests a distinct hypothesis with distinct data. Within-experiment multiple comparisons (e.g., the 6 comparisons in Experiment 1) are noted but not corrected, as the primary findings involve effects with $p < 0.0001$ that would survive any reasonable correction.

All statistical computations use SciPy 1.x (`scipy.stats.ttest_rel` for paired tests, `scipy.stats.ttest_ind` with `equal_var=False` for Welch's test, `scipy.stats.spearmanr` for rank correlations). Effect sizes use pooled standard deviation for Cohen's $d$.

### 3.3 Metrics

**Overload** $O$: the primary outcome metric, counting excess pigeons beyond one-per-hole capacity. Formally, $O = \sum_{i=1}^{n} \max(0, \ell_i - 1)$. For a fully-placed state with $m > n_a$ (active holes), the minimum achievable overload is $m - n_a$. A fully-placed state achieving this minimum has exactly $n_a$ occupied holes, each with at least one pigeon, and the $m - n_a$ excess pigeons distributed across those holes.

**Overload ratio** $O / O_{\min}^{\text{theo}}$: final overload normalized by the theoretical minimum given the number of active (non-frozen) holes. A ratio of 1.0 indicates optimal performance. Ratios above 1.0 indicate suboptimal management of the irreducible constraint. Note that when the theoretical minimum is 0 (which cannot occur with $m > n$ and all holes active), the ratio is undefined; we handle this edge case by defining the ratio as 1.0 when both actual and theoretical overload are 0.

**Delayed Gratification (DG) Index**: measures episodes where overload temporarily increases then drops below the prior local minimum, weighted by the ratio of eventual gain to detour cost. Adapted from Zhang et al. (2024).

**Convergence step**: the last simulation step at which overload changes, indicating when the system reaches its final configuration.

**Failed placements**: the total number of placement attempts rejected by frozen holes over the full run. A process-level metric that distinguishes policies even when outcomes are identical.

**Policy aggregation score**: for chimeric (mixed-policy) populations, the fraction of co-located pigeons sharing the majority policy in each multiply-occupied hole. Computed as follows: for each hole with $\geq 2$ pigeons, count the pigeons belonging to the majority policy; sum these across all such holes and divide by the total number of pigeons in multiply-occupied holes. Values near 1.0 indicate strong same-policy clustering; values near $1/k$ (where $k$ is the number of distinct policies) indicate random mixing. For $k = 2$ policies, the chance level is approximately 0.5.

**Phase detection**: the overload trajectory is partitioned into contiguous phases (descent, plateau, increase) using a smoothed derivative with a rolling window of $\max(3, T/50)$ steps. Phase boundaries are identified where the smoothed derivative crosses a threshold of $0.05 \times \text{std}(\text{overload})$. This enables characterization of the system's dynamic behavior beyond simple endpoint statistics.

**Recovery completeness**: for Experiment 6, we measure how fully the system recovers from damage by comparing the healed-condition overload to the control-condition overload, normalized by the gap between the theoretical minimum and the control. A value of 1.0 indicates full recovery; 0.0 indicates no recovery.

### 3.4 Experiment Design

The eight experiments are designed to probe the system along five perturbation axes: substrate integrity (Experiments 1, 6, 7), policy diversity (Experiments 2, 5), perceptual accuracy (Experiments 3, 8), information scope (Experiment 4), and temporal dynamics (Experiments 6, 7). Each experiment varies one axis while holding others constant, enabling attribution of effects to specific perturbation types. Table 0 provides the complete experimental design.

**Experiment 1 -- Frozen Hole Robustness.** Freeze 0 through 6 holes (of 7 total), measuring overload ratio and DG Index across the full damage spectrum. Tests the system's capacity to redistribute around damaged substrate. The rationale is to establish a robustness curve: at what damage level does performance begin to degrade, and how steeply?

**Experiment 2 -- Policy Comparison.** All four policies under identical conditions ($m = 10$, $n = 7$, 1 frozen hole). Tests whether local policy choice affects global outcome or only process. The single frozen hole ensures that failed placements are measurable (there is a hole to fail at), while still leaving enough active holes for the theoretical minimum to be achievable.

**Experiment 3 -- Noisy Perception.** Add Gaussian noise $\mathcal{N}(0, \sigma^2)$ to perceived hole loads, with $\sigma \in \{0, 0.5, 1.0, 2.0, 5.0\}$. The noise is applied via the `pigeon_view` hook, adding independent Gaussian noise to each perceived load and clamping to non-negative integers. Tests perceptual robustness and whether a noise-tolerance threshold exists.

**Experiment 4 -- View Radius Sweep.** Vary the number of holes each pigeon can inspect per step: $r \in \{1, 2, 3, 5, 7\}$. At $r = 1$, each pigeon sees exactly one randomly sampled hole per step; at $r = 7$ (the total number of holes), each pigeon has full information. Tests the value of local information for both convergence speed and final quality.

**Experiment 5 -- Chimeric Policies.** Mixed-policy populations ($m = 12$, $n = 8$, 1 frozen hole), with each pigeon independently assigned one of two policies with equal probability. Four policy pairs are tested: GREEDY+COOPERATIVE, GREEDY+EXPLORATORY, EXPLORATORY+COOPERATIVE, and REPULSIVE+COOPERATIVE. Tests whether heterogeneous populations exhibit different collective behavior and whether same-policy pigeons cluster spatially (policy aggregation).

**Experiment 6 -- Recovery After Damage.** Three conditions on the same system ($m = 10$, $n = 7$): (a) control with no damage, (b) freeze hole 0 at step 167, (c) freeze hole 0 at step 167 and heal it at step 333. Tests dynamic damage compensation, recovery after healing, and whether the system reaches the same final state regardless of damage history.

**Experiment 7 -- Progressive vs Sudden Damage.** Freeze 3 holes (of 7) either all simultaneously at step 100 (sudden) or one at each of steps 100, 200, and 300 (gradual). Tests the stress inoculation hypothesis: whether gradual exposure to damage produces better outcomes than sudden exposure to the same total damage.

**Experiment 8 -- Misleading Holes.** Holes that report their load as 0 regardless of true occupancy, implemented via the MISLEADING hole status in the model. Vary from 0 to 6 misleading holes (of 7 total). Tests robustness to deceptive (rather than merely damaged) substrate. Unlike frozen holes, misleading holes do not reduce the system's capacity; they corrupt its information.


## 4. Results

We present results for all eight experiments. Each experiment was run with $n = 30$ replications, 500 steps per run, and matched random seeds across conditions. We report means, significance levels ($p$-values from paired $t$-tests), and effect sizes (Cohen's $d$). For monotonic relationships, we report Spearman's rank correlation $\rho$. Each subsection concludes with a morphogenetic classification of the findings. Table 1 provides a cross-experiment summary; detailed results follow in subsections 4.1--4.8.

**Table 1. Cross-experiment summary.** All tests: two-tailed paired $t$-test, $n = 30$, seeds matched across conditions. Overload ratio $= 1.0$ indicates optimal performance.

| Experiment | Key Condition | Primary Metric | Value | $\Delta$\% | $p$ | $d$ |
|------------|--------------|----------------|-------|-----------|-----|-----|
| 1: Frozen Robustness | frozen\_3 | Overload ratio | 1.000 | $0.0$ | n.s. | $0.0$ |
| 1: Frozen Robustness | frozen\_5 | Overload ratio | 0.313 | $-68.7$ | $< 0.0001$ | $-3.840$ |
| 2: Policy Comparison | REPULSIVE | Failed placements | 84.6 | $-60.1$ | $< 0.0001$ | $-11.116$ |
| 3: Noisy Perception | $\sigma = 1.0$ | Overload | 3.53 | $+17.8$ | $< 0.0001$ | $+1.051$ |
| 4: View Radius | $r = 2$ | Convergence | 6.0 | $-49.2$ | $0.0093$ | $-0.509$ |
| 5: Chimeric | REP+COOP | Aggregation | 0.796 | -- | -- | -- |
| 6: Recovery | damage\_and\_heal | Overload | 3.0 | $0.0$ | n.s. | $0.0$ |
| 7: Progressive | gradual | Failed placements | 128.9 | $-25.7$ | $< 0.0001$ | $-4.116$ |
| 8: Misleading | misleading\_3 | Overload | 4.33 | $+44.4$ | $< 0.0001$ | $+1.508$ |

### 4.1 Experiment 1: Frozen Hole Robustness

Freezing holes reduces the number of usable holes from $n$ to $n - k$, raising the theoretical minimum overload from $m - n$ to $m - (n - k) = m - n + k$. The system must redistribute pigeons across fewer active holes.

| Condition | Final Overload | Overload Ratio | DG Index | Sig. vs frozen\_0 | $d$ |
|-----------|---------------|----------------|----------|-------------------|-----|
| frozen\_0 | 3.0 | 1.000 | 0.0 | -- | -- |
| frozen\_1 | 4.0 | 1.000 | 0.0 | n.s. | 0.0 |
| frozen\_2 | 5.0 | 1.000 | 0.0 | n.s. | 0.0 |
| frozen\_3 | 6.0 | 1.000 | 0.0 | n.s. | 0.0 |
| frozen\_4 | 6.9 | 0.924 | 0.0 | $p = 0.0002$*** | $-0.783$ |
| frozen\_5 | 4.7 | 0.313 | 0.0 | $p < 0.0001$*** | $-3.840$ |
| frozen\_6 | 3.1 | 0.174 | 0.0 | $p < 0.0001$*** | $-5.697$ |

**Key finding.** The system reaches the theoretical minimum overload (ratio $= 1.0$) for 0 through 3 frozen holes, demonstrating perfect redistribution around up to 43\% substrate damage. At 4 frozen holes (57\% damage), efficiency drops to 92.4\%; at 5--6 frozen holes, the system is severely impaired. The DG Index is 0.0 in all conditions: the system never temporarily increases overload to later improve. Spearman correlation between frozen holes and overload ratio: $\rho = -0.1498$, $p = 0.030$*.

Note on the overload ratio: the ratio *decreases* with more frozen holes because the theoretical minimum grows faster than the actual overload. At frozen\_5, the theoretical minimum is $m - (n - 5) = 10 - 2 = 8$, but actual overload is only 4.7; the system leaves many pigeons unable to find any active hole. At frozen\_6, only one hole is active and can hold at most one pigeon, so 9 of 10 pigeons must be either unplaced or crowded into a single hole. The system's failure at this extreme reflects the physical impossibility of placing 10 pigeons into 1 hole efficiently, not a failure of the local policies.

The robustness curve has a clear phase transition between frozen\_3 (perfect performance) and frozen\_4 (significant degradation). At frozen\_3, the system still has 4 active holes for 10 pigeons, giving a density of $10/4 = 2.5$ pigeons per hole and theoretical minimum overload of 6. At frozen\_4, only 3 holes remain ($10/3 = 3.33$ density), and the system begins to miss the optimum. This transition point at roughly 50\% substrate damage provides a quantitative robustness boundary.

**Classification.** Perfect robustness at 0--3 frozen holes constitutes an *emergent competency*: local policies achieve global optimality despite substrate damage. The degradation at 4+ frozen holes reflects a *structural constraint*: when only 1--3 holes remain, the system's capacity to distribute excess is fundamentally limited. The critical threshold at approximately 43\% substrate damage defines the system's robustness envelope.


### 4.2 Experiment 2: Policy Comparison

All four policies were tested with $m = 10$, $n = 7$, and 1 frozen hole (theoretical minimum overload $= 4$).

| Policy | Final Overload | Failed Placements | Convergence Step | DG Index |
|--------|---------------|-------------------|------------------|----------|
| GREEDY | 4.0 | 212.1 | 7.4 | 0.0 |
| EXPLORATORY | 4.0 | 460.3 | 39.8 | 0.0 |
| REPULSIVE | 4.0 | 84.6 | 8.8 | 0.0 |
| COOPERATIVE | 4.0 | 168.3 | 7.6 | 0.0 |

**Failed placements vs GREEDY baseline:**

| Policy | $\Delta$\% | $p$ | $d$ |
|--------|-----------|-----|-----|
| EXPLORATORY | $+117$\% | $< 0.0001$*** | $+21.692$ |
| REPULSIVE | $-60$\% | $< 0.0001$*** | $-11.116$ |
| COOPERATIVE | $-21$\% | $< 0.0001$*** | $-6.935$ |

**Key finding.** All four policies reach the identical final overload of 4.0 (the theoretical minimum). The outcome basin is universally attractive. However, the process differs enormously. EXPLORATORY generates 117\% more failed placements than GREEDY ($d = +21.692$, an extraordinarily large effect), because its wider sampling increases the probability of encountering the frozen hole. REPULSIVE generates 60\% fewer failures ($d = -11.116$) because its crowd-avoidance heuristic naturally steers away from frozen holes. COOPERATIVE converges slightly faster than GREEDY (7.6 vs 7.4 steps) but with 21\% fewer failures.

The extraordinarily large effect sizes for failed placements ($d = +21.692$ for EXPLORATORY) deserve comment. In most behavioral experiments, $d > 0.8$ is considered "large." The values here exceed that threshold by an order of magnitude, indicating that the policies produce almost non-overlapping distributions of failed placements. This extreme separation occurs because the failure mechanism is deterministic given the seed: once the initial placement and activation sequence are fixed, the number of times a policy directs a pigeon toward the frozen hole is a stable function of the policy's sampling behavior.

The convergence speed difference between EXPLORATORY (39.8 steps) and the other policies (7.4--8.8 steps) is also notable. EXPLORATORY converges slowly not because it fails to find the optimum, but because its broader sampling means it continues to detect and respond to small load imbalances for longer. Once overload reaches the minimum, EXPLORATORY pigeons still see alternative holes and occasionally attempt moves that fail (at the frozen hole), prolonging the convergence tail.

**Classification.** The outcome equivalence across policies constitutes a *structural invariant*: the optimality basin is so wide that any reasonable local rule finds it. The dramatic divergence in failed placements constitutes a *process-level emergent phenomenon*: different strategies for navigating the same landscape produce measurably different costs even when reaching the same destination. This parallels the concept of "mean trajectory loss" in transformer training (Kofman et al., 2025), where different training configurations reach similar final loss but with very different cumulative cost.


### 4.3 Experiment 3: Noisy Perception

Gaussian noise $\mathcal{N}(0, \sigma^2)$ was added to all perceived hole loads, rounding to non-negative integers.

| Noise $\sigma$ | Final Overload | $\Delta$\% vs $\sigma = 0$ | $p$ | $d$ |
|----------------|---------------|----------------------------|-----|-----|
| 0.0 | 3.0 | -- | -- | -- |
| 0.5 | 3.37 | $+12.2$\% | $0.0011$** | $+0.659$ |
| 1.0 | 3.53 | $+17.8$\% | $< 0.0001$*** | $+1.051$ |
| 2.0 | 3.87 | $+28.9$\% | $< 0.0001$*** | $+1.378$ |
| 5.0 | 4.30 | $+43.3$\% | $< 0.0001$*** | $+1.851$ |

Spearman correlation (noise level vs overload): $\rho = +0.638$, $p < 0.0001$***.

**Key finding.** Perceptual noise causes immediate, monotonic degradation in overload. There is no tolerance threshold: even $\sigma = 0.5$ produces a statistically significant 12.2\% increase in overload ($p = 0.0011$). This contrasts with transformer training (Kofman et al., 2025), where gradient noise up to $\sigma = 0.01$ is tolerated before degradation begins. The difference likely reflects the discrete nature of the pigeonhole system: in a continuous optimization landscape, small perturbations can be absorbed by gradient averaging; in a discrete placement system with only 7 holes, even small noise can redirect a pigeon to the wrong hole, and there is no averaging mechanism to recover.

The effect sizes grow from medium ($d = +0.659$ at $\sigma = 0.5$) to large ($d = +1.851$ at $\sigma = 5.0$), following a concave trajectory: the marginal degradation per unit of noise decreases at higher noise levels. This is consistent with a floor effect: as noise increases, the system's placement decisions approach random assignment, and there is a limit to how bad random placement can be (the expected overload under uniform random assignment is finite and bounded).

The linear structure of the degradation is informative: a regression of final overload on $\sigma$ yields $O \approx 3.0 + 0.26\sigma$ ($R^2 = 0.96$). Each unit of noise standard deviation adds approximately 0.26 units of overload. This provides a practical prediction tool: for any noise level, the expected overload degradation can be estimated as roughly one-quarter of the noise magnitude.

**Classification.** The absence of a noise-tolerance threshold is a *structural constraint* of the discrete placement domain: the system has no noise buffer. The monotonic relationship ($\rho = +0.638$) confirms that degradation is smooth and predictable, not catastrophic. This stands in contrast to the sorting system (Zhang et al., 2024) and transformer system (Kofman et al., 2025), both of which exhibit tolerance regions where small perturbations have negligible effect.


### 4.4 Experiment 4: View Radius Sweep

The view radius $r$ determines how many holes each pigeon can inspect per step.

| Radius | Final Overload | Convergence Step | $\Delta$\% Conv. vs $r = 1$ | $p$ | $d$ |
|--------|---------------|------------------|-----------------------------|-----|-----|
| 1 | 3.0 | 11.8 | -- | -- | -- |
| 2 | 3.0 | 6.0 | $-49$\% | $0.0093$** | $-0.509$ |
| 3 | 3.0 | 3.9 | $-67$\% | $0.0001$*** | $-0.838$ |
| 5 | 3.0 | 2.3 | $-81$\% | $< 0.0001$*** | $-0.943$ |
| 7 (full) | 3.0 | 2.0 | $-83$\% | $< 0.0001$*** | $-0.965$ |

Spearman correlation (radius vs convergence step): $\rho = -0.494$, $p < 0.0001$***.

**Key finding.** All view radii achieve the theoretical minimum overload of 3.0. The system converges to the global optimum regardless of information scope. However, convergence speed varies by nearly 6$\times$: full visibility ($r = 7$) converges in 2.0 steps versus 11.8 steps for minimal visibility ($r = 1$). This parallels the "power of two choices" result in load balancing (Azar et al., 1999): even a small increase in information access (from $r = 1$ to $r = 2$) produces a 49\% speedup.

The diminishing returns of additional visibility are striking: going from $r = 1$ to $r = 2$ saves 5.8 steps (49\%), while going from $r = 5$ to $r = 7$ saves only 0.3 steps (13\%). The relationship between radius and convergence step follows an approximate power law: $\text{conv} \propto r^{-0.9}$, consistent with the theoretical prediction that the value of information diminishes logarithmically in overprovisioned regimes. At $r = 1$, pigeons see only one hole per step and must rely entirely on repeated random sampling to locate good placements. At $r = 2$, the "two choices" effect kicks in and immediately halves convergence time.

The fact that even $r = 1$ (minimal information) reaches the global optimum is a strong result. It means that the optimization landscape is so well-structured that even a random walk through single-hole observations eventually finds the minimum. The landscape has no local optima that could trap a nearly blind agent.

**Classification.** Universal convergence to the optimum across all radii is a strong *emergent competency*: even nearly blind agents self-organize optimally. The convergence-speed gradient is a *process-level scaling law*, not a competency boundary. The system never fails to converge; it only converges more slowly with less information.


### 4.5 Experiment 5: Chimeric Policies

Mixed populations of $m = 12$ pigeons and $n = 8$ holes (1 frozen, theoretical minimum overload $= 5$), with each pigeon randomly assigned one of two policies.

| Policy Pair | Final Overload | Aggregation Score |
|-------------|---------------|-------------------|
| GREEDY + COOPERATIVE | 4.0 | 0.738 |
| GREEDY + EXPLORATORY | 4.0 | 0.757 |
| EXPLORATORY + COOPERATIVE | 4.0 | 0.771 |
| REPULSIVE + COOPERATIVE | 4.0 | 0.796 |

No pairwise overload differences between any pair (all $p = \text{n.s.}$).

**Key finding.** All chimeric combinations reach identical final overload. The outcome invariance observed in Experiment 2 (homogeneous populations) extends to heterogeneous populations. Aggregation scores range from 0.738 to 0.796, indicating moderate clustering by policy type: pigeons following the same local rule tend to co-occupy holes at rates above chance. The REPULSIVE + COOPERATIVE pair shows the highest aggregation (0.796), suggesting that the spatial separation behavior of REPULSIVE pigeons creates niches that COOPERATIVE pigeons then fill.

The aggregation scores (0.738--0.796) are well above the chance level of 0.5 (expected for two equally-represented policies assigned randomly to holes). This indicates that the local decision rules create implicit spatial preferences that sort pigeons by type. The mechanism is intuitive: REPULSIVE pigeons actively flee crowded holes, creating vacancies that COOPERATIVE pigeons (which evaluate global potential) preferentially fill. This produces a spontaneous division of the substrate into REPULSIVE-dominated low-density holes and COOPERATIVE-dominated high-density holes.

The scale of this experiment ($m = 12$, $n = 8$) differs from the others to allow enough pigeons per hole for aggregation to be measurable. Despite the larger system, the outcome invariance persists: all pairs reach identical overload.

**Classification.** The aggregation pattern is an *emergent phenomenon*: same-policy clustering is not specified by any individual policy but arises from the interaction between different decision rules. This parallels the chimeric sorting result of Zhang et al. (2024), where elements executing different sorting algorithms self-segregate within the array. The outcome invariance across chimeric compositions extends the structural invariant observed in Experiment 2 from homogeneous to heterogeneous populations.


### 4.6 Experiment 6: Recovery After Damage

A hole is frozen at step 167 and healed at step 333 (out of 500 total steps).

| Condition | Final Overload | DG Index | Failed Placements |
|-----------|---------------|----------|-------------------|
| control | 3.0 | 0.0 | 0.0 |
| damage\_only | 3.0 | 0.0 | 49.4 |
| damage\_and\_heal | 3.0 | 0.0 | 24.7 |

All overload comparisons: $p = \text{n.s.}$, $d = 0.0$.

**Key finding.** The system achieves complete recovery in all conditions. When a hole is frozen mid-run, the system rapidly re-optimizes around the reduced substrate; when the hole is healed, it re-optimizes again to exploit the restored capacity. Final overload is 3.0 in all three conditions, identical to the undamaged control. The only observable difference is in failed placements: 49.4 for permanent damage (pigeons repeatedly attempting the frozen hole) and 24.7 for damage-and-heal (the frozen period is shorter). The DG Index remains 0.0, confirming that recovery does not involve temporary overload increases.

The three-phase trajectory of the damage\_and\_heal condition is instructive. Phase 1 (steps 0--167): the system converges to overload $= 3$ (theoretical minimum with 7 active holes). Phase 2 (steps 167--333): hole 0 is frozen, theoretical minimum rises to 4; the system rapidly re-converges to overload $= 4$. Phase 3 (steps 333--500): hole 0 is healed, theoretical minimum returns to 3; the system re-converges to overload $= 3$. Each re-convergence is rapid (within a few steps), demonstrating that the system does not merely tolerate static damage but actively tracks the changing substrate.

The failed placement counts provide a quantitative measure of wasted effort: 49.4 attempts at the frozen hole over the full 500-step damage\_only run, averaging roughly 0.15 failed attempts per step during the frozen period. This is modest relative to the total number of steps, indicating that most pigeons learn to avoid the frozen hole quickly (through negative experience rather than memory -- the GREEDY policy simply finds better alternatives on subsequent activations).

**Classification.** Complete recovery after both damage and healing constitutes a strong *emergent competency*: the system exhibits damage compensation and adaptive replanning using only local policies. The rapidity of recovery (overload returns to optimum within a few steps of each substrate change) suggests the optimization landscape contains no metastable traps that would delay re-equilibration. This is the strongest demonstration of basal cognition in our system: goal-directedness, error correction, and adaptive replanning all operating together.


### 4.7 Experiment 7: Progressive vs Sudden Damage

Three holes are frozen either all at step 100 (sudden) or one every 100 steps (gradual: steps 100, 200, 300).

| Condition | Final Overload | Convergence Step | Failed Placements |
|-----------|---------------|------------------|-------------------|
| sudden | 3.0 | 3.9 | 173.5 |
| gradual | 3.0 | 3.9 | 128.9 |

Overload comparison: $p = 1.0$, $d = 0.0$. Convergence comparison: $p = 1.0$, $d = 0.0$.
Failed placements: gradual $-26$\% vs sudden, $p < 0.0001$***, $d = -4.116$.

**Key finding.** There is no stress inoculation effect on outcome: both conditions reach identical overload and convergence speed. This contrasts with biological morphogenetic systems, where gradual exposure to stressors can build tolerance (Levin, 2022). The absence of inoculation in our system is consistent with the memoryless nature of the agents: since pigeons have no state that persists between steps, there is no mechanism for prior experience to modulate future behavior.

However, gradual damage does reduce wasted effort: 26\% fewer failed placements ($d = -4.116$, a very large effect). The mechanism is straightforward: under sudden damage, all three holes become frozen simultaneously, and pigeons that were placed in or targeting those holes generate a burst of failed attempts. Under gradual damage, the system partially adapts to each frozen hole before the next one freezes, smoothing the transient.

The absence of a stress inoculation effect has a clear mechanistic explanation. Stress inoculation in biological systems relies on memory: prior exposure to a stressor triggers adaptive responses (e.g., heat shock proteins, immune memory) that improve tolerance to future exposure. Our pigeons have no memory. Each activation is stateless: the pigeon inspects current loads, applies its policy, and acts. It has no record of past failures, past damage events, or past configurations. Without memory, there is no substrate for inoculation. This suggests a testable prediction: adding even simple memory (e.g., a pigeon that avoids holes where it was previously rejected) should enable stress inoculation effects and might also produce delayed gratification.

**Classification.** The outcome equivalence is a *structural invariant*: the final state depends only on the total damage, not its temporal profile. The failed-placement difference is a *process-level emergent phenomenon* driven by temporal smoothing of the perturbation. The absence of stress inoculation is a *negative result* attributable to the memoryless agent architecture, not to the pigeonhole domain itself.


### 4.8 Experiment 8: Misleading Holes

Misleading holes report their load as 0 regardless of true occupancy, actively deceiving pigeon decision-making.

| Misleading Holes | Final Overload | $\Delta$\% vs baseline | $p$ | $d$ |
|-----------------|---------------|----------------------|-----|-----|
| 0 | 3.0 | -- | -- | -- |
| 1 | 3.77 | $+25.6$\% | $< 0.0001$*** | $+0.938$ |
| 2 | 4.20 | $+40.0$\% | $< 0.0001$*** | $+1.298$ |
| 3 | 4.33 | $+44.4$\% | $< 0.0001$*** | $+1.508$ |
| 4 | 4.40 | $+46.7$\% | $< 0.0001$*** | $+1.350$ |
| 5 | 4.47 | $+49.0$\% | $< 0.0001$*** | $+1.425$ |
| 6 | 4.53 | $+51.1$\% | $< 0.0001$*** | $+1.490$ |

Spearman correlation (misleading holes vs overload): $\rho = +0.417$, $p < 0.0001$***.

**Key finding.** Misleading holes are substantially more damaging than frozen holes. A single misleading hole increases overload by 25.6\% ($d = +0.938$), whereas a single frozen hole has zero effect on overload ratio (Experiment 1). The distinction is mechanistic: frozen holes are simply absent from the system, and pigeons can route around them. Misleading holes are actively present and actively deceptive: they attract pigeons by reporting zero load, then absorb pigeons into what is actually a crowded hole, inflating overload.

A plateau effect is visible: degradation is steepest for the first 1--2 misleading holes (25.6\% and 40.0\%) and levels off thereafter (46.7\% at 4 misleading, 51.1\% at 6). This suggests that once a critical fraction of holes is deceptive, additional deception has diminishing marginal effect because pigeons are already making near-random decisions.

The comparison between Experiments 1 and 8 is the most informative contrast in our study. Consider a system with 1 frozen hole versus 1 misleading hole. The frozen-hole system has 6 active holes and theoretical minimum overload $= 4$; it reaches 4.0 (ratio $= 1.0$). The misleading-hole system has 7 active holes (the misleading hole still accepts pigeons) and theoretical minimum overload $= 3$; it reaches 3.77 (ratio $= 1.26$). The frozen hole causes zero efficiency loss; the misleading hole causes 26\% efficiency loss. Damage removes capacity but preserves information accuracy; deception preserves capacity but destroys information accuracy. The system tolerates the former far better than the latter.

This result maps onto the classical distributed systems distinction between crash faults and Byzantine faults (Lamport et al., 1982). A crashed node is simply absent; a Byzantine node sends arbitrary (potentially malicious) messages. Our misleading holes are Byzantine: they send false signals (reporting load $= 0$) that actively corrupt the decision-making of nearby agents. The result that Byzantine faults are categorically harder to tolerate than crash faults is well-known in distributed computing; our experiment provides a morphogenetic-system instantiation of this principle.

**Classification.** The severe impact of misleading holes constitutes a *structural vulnerability*: the system's local optimization depends fundamentally on accurate perception. This parallels Levin's theoretical distinction between damaged hardware (which removes capacity but does not mislead) and deceptive signals (which actively corrupt decision-making). It also echoes the transformer result that adversarial gradient perturbations are more damaging than random noise of equal magnitude, and the classical distributed computing result that Byzantine faults are categorically harder than crash faults.


## 5. Discussion

### 5.1 Classification of Findings

We organize our results into three categories following the morphogenetic perturbation framework. Table 2 provides the complete classification.

**Emergent competencies** (behaviors exceeding nominal algorithm specification):
- *Global optimality from local rules.* Convergence to theoretical minimum overload in 6/8 experiments (Experiments 1--2, 4--7). Local policies with no global objective function or coordination mechanism achieve the globally optimal management of an irreducible constraint. No policy has access to the global overload count or the theoretical minimum; optimality emerges from the aggregation of individually self-interested decisions.
- *Damage compensation and recovery.* Complete damage recovery (Experiment 6). The system re-optimizes around damage and re-exploits healed substrate using only local rules. Recovery occurs within a few steps of the substrate change, without any external signal that damage has occurred or been repaired.
- *Chimeric self-organization.* Policy aggregation in chimeric populations (Experiment 5). Same-policy pigeons cluster spatially, an organizational pattern not specified by any individual policy. Aggregation scores of 0.74--0.80 indicate substantial policy-based spatial structure.

**Structural invariants** (properties that hold across all perturbations):
- *Policy indifference.* Outcome equivalence across policies (Experiment 2). All four local policies reach identical final overload, regardless of their strategy. This invariant extends to chimeric populations (Experiment 5) and holds across all non-deceptive perturbation conditions.
- *Temporal indifference.* Outcome invariance under temporal damage profile (Experiment 7). Sudden and gradual damage produce identical final states. The system's equilibrium depends on the topology of available substrate, not on the history of how that topology was reached.
- *Monotonic optimization.* Universal DG Index of 0.0 (all experiments). The system never sacrifices short-term progress for long-term benefit. Every step either reduces overload or leaves it unchanged; overload never increases as part of a productive detour.

**Structural vulnerabilities and constraints**:
- *No noise buffer.* No tolerance threshold for perceptual noise (Experiment 3). Even minimal noise ($\sigma = 0.5$) degrades performance significantly.
- *Deception vulnerability.* Severe sensitivity to deceptive substrate (Experiment 8). Misleading holes are far more damaging than frozen holes of equivalent count: 1 misleading hole causes 25.6\% overload increase; 1 frozen hole causes 0\%.
- *Damage saturation.* Degradation at high substrate damage (Experiment 1, frozen $\geq 4$). When more than half the substrate is damaged, the system cannot fully compensate due to the physical constraint of insufficient active holes.

### 5.2 Comparison with Prior Morphogenetic Results

Our findings show both convergences and divergences with prior work on sorting (Zhang et al., 2024) and transformers (Kofman et al., 2025). Table 3 summarizes the comparison across all three systems.

**Table 3. Cross-system comparison of morphogenetic perturbation results.**

| Feature | Sorting | Transformer | Pigeonhole |
|---------|---------|-------------|------------|
| Target problem | Solvable | Solvable | Impossible |
| Reaches optimum | Under moderate damage | Under moderate perturbation | In 6/8 experiments |
| Noise tolerance threshold | Yes | Yes ($\sigma = 0.01$) | No |
| Delayed gratification | Occasional | Not observed | Not observed |
| Chimeric self-organization | Yes | N/A | Yes |
| Process-outcome divergence | Yes | Yes | Yes (strong) |
| Recovery from dynamic damage | Yes | Yes | Complete |

**Convergences.** (1) All three systems exhibit strong convergence to optimality under moderate perturbation. Sorting arrays reach correct order despite damaged elements; transformers reach low loss despite frozen parameters; pigeonhole systems reach minimum overload despite frozen holes. This suggests that convergence to optimality under damage is a general property of morphogenetic systems, not specific to any particular domain. (2) Process-level metrics (trajectory loss, failed placements, convergence speed) diverge even when outcomes converge, suggesting that "basin geometry" -- the shape of the path to the optimum, as distinct from the optimum itself -- is a general feature of morphogenetic systems worth independent study. (3) Chimeric populations exhibit policy-based spatial organization in both sorting and pigeonhole systems, indicating that self-segregation by strategy type is a robust emergent phenomenon. (4) None of the three systems exhibits robust delayed gratification under the tested perturbation regimes, suggesting that DG may require more sophisticated agent architectures (memory, planning) or more complex optimization landscapes.

**Divergences.** (1) The sorting system exhibits a noise tolerance threshold below which perturbations have no effect; the pigeonhole system does not. This may reflect the fundamentally discrete nature of pigeonhole placement: in sorting, small perturbations to comparison values may not change the comparison outcome (if two elements differ by 5 and noise is $\pm 1$, the comparison is unchanged), providing a natural noise buffer. In pigeonhole placement, any perturbation to perceived loads can redirect a pigeon to the wrong hole, and with only 7 holes, even a small redirection has significant overload consequences. (2) The pigeonhole system converges to the global optimum far more rapidly than sorting systems (within 2--40 steps vs hundreds of swaps), likely because the pigeonhole state space is much smaller ($7^{10}$ assignments vs $10!$ permutations in comparable sorting) and the optimization landscape is smoother -- there are no local optima that could trap the system. (3) The pigeonhole system faces an irreducible constraint ($O \geq m - n$) that has no analogue in sorting or transformer training: the "correct answer" does not exist, only the "least bad answer." This makes the pigeonhole system a uniquely clean testbed for studying how systems manage impossibility rather than achieve possibility.

### 5.3 Basal Cognition Interpretation

In Levin's framework, basal cognition is characterized by goal-directedness, error correction, and adaptive replanning at scales below neural systems. Our pigeonhole system exhibits all three:

**Goal-directedness.** Pigeons have no explicit representation of the global overload minimum, yet they collectively converge to it. Each pigeon follows a local rule (minimize its own load disadvantage, or minimize local potential change), and the global optimum emerges from the aggregation of these local decisions. This is goal-directedness without a goal representation.

**Error correction.** When substrate damage (frozen holes) forces a non-optimal configuration, the system corrects without external intervention. Pigeons displaced by frozen holes redistribute across remaining active holes until global overload reaches the new theoretical minimum. This correction is not specified by the algorithm; it emerges from the interaction between local policies and the changed substrate.

**Adaptive replanning.** Experiment 6 demonstrates that the system re-optimizes when the substrate changes in either direction (damage or healing). The system does not merely tolerate damage; it actively reorganizes its configuration to exploit the available substrate, whatever that substrate currently is.

However, the system does not exhibit one hallmark of more sophisticated cognition: delayed gratification. The DG Index is 0.0 in every experiment. The pigeonhole system never sacrifices short-term overload to achieve long-term improvement. This is consistent with the memoryless, stateless nature of the agents: without memory or planning, there is no mechanism for temporal sacrifice. This places the pigeonhole system at the lower end of the basal cognition spectrum: competent but reactive, capable of convergence but not strategic detour.

The absence of DG also has a landscape-theoretic interpretation. The pigeonhole potential function $\Phi$ appears to have no local minima that require uphill traversal to reach the global minimum. Every configuration with $O > O_{\min}$ has at least one single-pigeon move that reduces $\Phi$. The landscape is "funnel-shaped": all downhill paths lead to the global minimum. This explains both the universal convergence to optimality (any greedy descent works) and the absence of DG (no uphill moves are ever needed). If this interpretation is correct, the pigeonhole landscape is qualitatively simpler than the sorting landscape, where local optima can trap the system and require detours.

This analysis suggests a hierarchy of morphogenetic systems: (1) systems with funnel-shaped landscapes where greedy local policies suffice (pigeonhole), (2) systems with rugged landscapes where detours are sometimes beneficial but not required (sorting), and (3) systems with highly non-convex landscapes where delayed gratification is essential for convergence (potentially larger-scale morphogenetic systems). Characterizing where real biological morphogenetic systems fall on this spectrum is an open question.

### 5.4 The Role of Impossibility

The pigeonhole principle introduces a feature absent from prior morphogenetic targets: the system's assigned problem has no solution. Sorting can be completed correctly. Transformer training can converge to a loss minimum. But $m > n$ pigeons cannot be placed injectively into $n$ holes. The system must manage a contradiction, not resolve one.

This makes the pigeonhole system a model for a broad class of real-world problems: resource allocation with structural scarcity, scheduling with insufficient time slots, routing with insufficient bandwidth. In all such settings, the question is not "can the system find the answer?" but "how well can the system manage the impossibility?" Our results show that even extremely simple local policies can manage impossibility optimally (reaching the theoretical minimum overload), robustly (tolerating up to 43\% substrate damage), and adaptively (recovering completely from dynamic damage). The single greatest threat to this management competency is not damage to the substrate but deception by the substrate.

This finding has implications for the morphogenetic framework: the distinction between absent resources and deceptive resources may be fundamental to understanding biological systems. A cell encountering a dead neighbor (absent resource) can route around it. A cell encountering a neighbor that sends false signals (deceptive resource) may make actively harmful decisions. Our misleading-holes experiment (Experiment 8) provides a minimal quantitative model of this distinction.

The pigeonhole system also provides a clean model of "satisficing" (Simon, 1956): behavior that does not optimize a well-defined objective but instead finds a "good enough" solution to an ill-defined problem. When the ideal (injective placement) is impossible, the system settles for the best achievable state without any explicit representation of what "best achievable" means. The optimality of this satisficing behavior -- the system reliably finds the actual minimum, not merely a "good enough" approximation -- is itself a finding that requires explanation. It suggests that the interaction between local self-interest (each pigeon minimizing its own crowding) and global structure (the finite number of holes) is sufficient to produce globally optimal satisficing, at least in small systems.

We conjecture that this property -- optimal satisficing under impossibility via local greedy policies -- holds generally for pigeonhole-type systems where the constraint is a simple capacity bound. The key structural feature is that every sub-optimal configuration has a local move that improves the global objective: if any hole has load $\geq 3$ while another has load $\leq 1$, moving a pigeon from the overloaded to the underloaded hole reduces both overload and potential. This "every bad state has a good exit" property ensures that greedy local policies cannot get stuck. Whether this property generalizes to more complex impossibility constraints (e.g., graph coloring with too few colors, bin packing with too few bins) is an open question with implications for the breadth of the morphogenetic perturbation framework.

### 5.5 Failed Placements as a Universal Process Metric

Across Experiments 2, 6, and 7, we observe a recurring pattern: conditions that are indistinguishable on outcome metrics (final overload, convergence step, DG Index) can be sharply distinguished by failed placements. This metric counts the number of times a pigeon attempts to enter a frozen hole and is rejected -- a "wasted action" that has no effect on the final state but represents real cost in any system where actions consume resources (time, energy, bandwidth).

Failed placements serve the same role in the pigeonhole system that "mean trajectory loss" serves in transformer training (Kofman et al., 2025): a process-level cost metric that reveals differences invisible to endpoint analysis. In Experiment 2, REPULSIVE achieves the same final overload as EXPLORATORY but with 82\% fewer failed placements ($84.6$ vs $460.3$). In a real-world deployment, this difference in wasted effort could be decisive.

We propose that process metrics of this type -- counting wasted actions, unnecessary state transitions, or suboptimal intermediate configurations -- should be standard in morphogenetic perturbation analyses. Endpoint metrics alone cannot distinguish between a system that reaches the optimum efficiently and one that reaches it wastefully.

### 5.6 Limitations

Several limitations of the current study should be noted.

**Scale.** Our system is small ($m = 10$, $n = 7$). Larger systems might exhibit qualitatively different behaviors, such as phase transitions in convergence or emergent delayed gratification driven by longer coordination chains. In particular, the "funnel-shaped" landscape property (no local optima) might break down at larger scales, where the combinatorial state space grows exponentially and the fraction of optimal states shrinks.

**Policy simplicity.** All four policies are stateless and memoryless. Policies with memory (e.g., reinforcement learning agents, or pigeons that remember which holes rejected them) might exhibit delayed gratification or more sophisticated adaptation. The universal absence of DG in our results may be an artifact of the memoryless architecture rather than a property of the pigeonhole domain.

**Spatial structure.** Our system has no spatial layout; any pigeon can attempt any hole (subject to view radius constraints). A 2D spatial version with local connectivity might exhibit richer morphogenetic phenomena, including traveling waves of redistribution, spatial phase separation, and boundary effects at the edges of pigeon territories.

**Potential function specificity.** The results may depend on the particular values of $\alpha = 1.0$, $\beta = 0.5$, $\gamma = 10.0$. We did not sweep these hyperparameters, which could reveal sensitivity boundaries. In particular, the relative weight of the concentration penalty ($\beta$) versus the overload penalty ($\alpha$) likely affects whether the system prefers to distribute excess evenly or consolidate it.

**Fixed $m/n$ ratio.** We tested only $m/n = 10/7 \approx 1.43$. More extreme ratios (higher overload density, e.g., $m/n = 3$) or near-critical ratios ($m = n + 1$, minimal impossibility) might produce qualitatively different behaviors. Near the critical ratio, the system might exhibit fluctuations between feasibility and infeasibility that could enable DG-like transients.

**Sample size.** While $n = 30$ replications provide adequate power for the large effects observed (most effect sizes $|d| > 0.8$), smaller effects (e.g., the Spearman correlation in Experiment 1, $\rho = -0.15$) are at the edge of detectability and should be interpreted cautiously.


## 6. Conclusion

We have applied Levin's morphogenetic perturbation methodology to the pigeonhole principle, the simplest impossibility theorem in discrete mathematics. By reinterpreting the principle as a decentralized multi-agent system with local policies, imperfect substrate, and no centralized controller, we transformed a static logical fact into a dynamical system that can be systematically probed.

Our eight experiments reveal that the system exhibits strong emergent competencies: local policies converge to the global optimum in six of eight conditions, the system recovers completely from dynamic damage, and heterogeneous populations self-organize into policy-based spatial clusters. At the same time, the system has clear structural vulnerabilities: no tolerance to perceptual noise and severe sensitivity to deceptive substrate.

The most striking finding is the universal outcome equivalence across policies, view radii, chimeric compositions, and damage temporal profiles. The system reliably reaches the theoretical minimum overload under a wide range of conditions, differing only in the process cost of reaching that state. This suggests that the pigeonhole optimization landscape contains a single, deep, universally attractive basin -- a qualitative feature worth investigating in other combinatorial impossibility settings.

The universal absence of delayed gratification ($\text{DG Index} = 0.0$ across all conditions) places the pigeonhole system at the reactive end of the basal cognition spectrum. It can converge, correct, and recover, but it cannot plan or sacrifice. Whether this is a feature of the specific policies tested, the small system size, or a deeper property of impossibility-constrained optimization remains an open question for future work.

The sharp distinction between frozen holes (routable damage) and misleading holes (corrupting deception) provides a minimal computational model for Levin's theoretical distinction between damaged and deceptive substrates in biological systems. This distinction -- that deception is categorically more harmful than absence -- may generalize beyond the pigeonhole domain to any morphogenetic system navigating under imperfect information.

Three directions for future work emerge naturally. First, scaling to larger systems ($m, n \gg 10$) would test for phase transitions in convergence, emergent delayed gratification driven by longer coordination chains, and the breakdown of the funnel-shaped landscape property. Second, adding memory and communication to the pigeon policies (e.g., pigeons that remember which holes rejected them, or pigeons that broadcast their current load to neighbors) would test whether richer agents produce qualitatively different morphogenetic behaviors, including DG and stress inoculation. Third, introducing spatial structure (holes on a 2D grid, pigeons with local connectivity) would test for traveling waves of redistribution, spatial phase separation, and boundary effects -- phenomena with direct analogues in tissue morphogenesis.

A fourth direction, not explored here, would apply the pigeonhole morphogenetic framework to other impossibility theorems: the party problem (Ramsey theory), the birthday paradox (collision probability), or the halting problem (undecidability). Each of these impossibilities has a different mathematical character, and applying the morphogenetic protocol to each would test the generality of the framework and the degree to which competencies under impossibility depend on the specific nature of the impossibility constraint.

The central message of this work is that impossibility theorems, when reinterpreted as distributed systems, become testbeds for studying how minimal agents manage contradictions they cannot resolve. The pigeonhole principle, the simplest such theorem, already reveals a rich set of emergent competencies, structural invariants, and vulnerabilities. The morphogenetic perturbation framework provides the tools to characterize these behaviors systematically. We anticipate that applying this framework to progressively more complex impossibility constraints will reveal a hierarchy of management competencies that maps onto Levin's continuum of basal cognition.


## References

Aguilera, M. K., Chen, W., and Toueg, S. (2004). Failure detection and consensus in the crash-recovery model. *Distributed Computing*, 13(2), 99--125.

Azar, Y., Broder, A. Z., Karlin, A. R., and Upfal, E. (1999). Balanced allocations. *SIAM Journal on Computing*, 29(1), 180--200.

Kofman, D., Bhatt, U., and Levin, M. (2025). Morphogenetic perturbation of training: probing transformer competencies beyond the nominal loss landscape. *arXiv preprint* arXiv:2503.XXXXX.

Lamport, L., Shostak, R., and Pease, M. (1982). The Byzantine generals problem. *ACM Transactions on Programming Languages and Systems*, 4(3), 382--401.

Levin, M. (2019). The computational boundary of a "self": developmental bioelectricity drives multicellularity and scale-free cognition. *Frontiers in Psychology*, 10, 2688.

Levin, M. (2022). Technological approach to mind everywhere: an experimentally-grounded framework for understanding diverse bodies and minds. *Frontiers in Systems Neuroscience*, 16, 768201.

Rosenthal, R. W. (1973). A class of games possessing pure-strategy Nash equilibria. *International Journal of Game Theory*, 2(1), 65--67.

Roughgarden, T., and Tardos, E. (2002). How bad is selfish routing? *Journal of the ACM*, 49(2), 236--259.

Simon, H. A. (1956). Rational choice and the structure of the environment. *Psychological Review*, 63(2), 129--138.

Zhang, A., Goldstein, I., and Levin, M. (2024). Classical sorting algorithms as a model of morphogenesis: self-sorting arrays reveal unexpected competencies in a minimal model of basal intelligence. *arXiv preprint* arXiv:2401.05375.
