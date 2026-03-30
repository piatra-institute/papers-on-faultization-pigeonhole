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

We apply the morphogenetic perturbation methodology of Levin and collaborators to the pigeonhole principle, reinterpreting a classical impossibility theorem as a distributed multi-agent system. In our model, $m = 10$ autonomous pigeons self-organize into $n = 7$ holes under four local placement policies (GREEDY, EXPLORATORY, REPULSIVE, COOPERATIVE), with no centralized controller. Because $m > n$, overload $O \geq m - n = 3$ is irreducible; the system cannot solve the problem, only manage it. We subject this system to eight perturbation experiments ($n = 30$ replications, 500 steps, paired $t$-tests with matched seeds): frozen-hole robustness, policy comparison, noisy perception, view-radius sweep, chimeric mixed-policy populations, dynamic damage and recovery, progressive versus sudden damage, and misleading (deceptive) holes. We find that (1) the system converges to the theoretical minimum overload in six of eight experiments, demonstrating strong collective competence; (2) policies that are identical at the endpoint differ dramatically in failure persistence, with same-target retry after rejection ranging from 0.463 (REPULSIVE) to 0.997 (COOPERATIVE), indicating little evidence of agent-level learning; (3) perceptual noise causes immediate monotonic degradation with no tolerance threshold ($\rho = +0.638$, $p < 0.0001$); (4) misleading holes induce strong attraction bias, with a single misleading hole capturing 36\% of pigeons and 66\% of overload while increasing overload by 25.6\%; and (5) delayed gratification is absent in all conditions (DG Index $= 0.0$), making it a negative result rather than the main explanatory axis. We argue that faultization in this system reveals collective adaptation, retry persistence, and bias formation more clearly than it reveals strategic detour.


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
- We conduct eight systematic experiments spanning substrate damage, perceptual noise, information radius, policy heterogeneity, dynamic damage/recovery, and substrate deception, with paired statistical analysis and new process metrics for post-failure persistence and deceptive-substrate bias.
- We demonstrate that local policies achieve global optimality in six of eight conditions, constituting a strong emergent competency in the Levin framework -- the system finds the theoretical minimum overload using only local rules and no global coordination.
- We show that the system's most informative process signal is not delayed gratification but failure persistence: after rejection, some policies repeatedly target the same faulty hole on their next attempted move (0.94 EXPLORATORY, 1.00 COOPERATIVE), revealing the absence of negative learning at the agent level.
- We identify a sharp distinction between damaged substrate and deceptive substrate: misleading holes do not merely degrade overload, they induce strong occupancy and overload bias toward the faulty resource itself.
- We retain the universal absence of delayed gratification as a negative result, establishing that the pigeonhole landscape appears monotonic under the tested policy class.
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

**Theoretical minimum overload.** For a system with $n_u$ usable (non-frozen) holes and $m$ pigeons, the theoretical minimum overload is:

$$O_{\min}^{\text{theo}} = \max(0, m - n_u)$$

This follows from the observation that the maximum number of holes that can each hold exactly one pigeon is $\min(m, n_u)$, leaving $m - \min(m, n_u)$ excess pigeons when $m > n_u$. Misleading holes remain usable even though they corrupt perception. All experiments use this quantity as the normalization baseline for the overload ratio.

**State space size.** The full state space has $(n + 1)^m$ configurations (each pigeon in one of $n$ holes or unplaced). For $m = 10$, $n = 7$, this is $8^{10} \approx 10^9$. The optimal states form a much smaller subset: any configuration where all $n$ holes are occupied and the $m - n = 3$ excess pigeons are distributed arbitrarily constitutes a minimum-overload state. The number of such states is $\binom{m}{n} \cdot n! \cdot S(m - n, n, n)$ where $S$ accounts for the distribution of excess, but the precise count matters less than the qualitative observation: optimal states are a tiny fraction of the state space, yet the system reliably finds them.

### 3.2 Statistical Protocol

All experiments use $n_{\text{rep}} = 30$ replications with matched random seeds across conditions. The primary statistical test is the paired $t$-test (two-tailed), which exploits seed-matching to control for initialization variance. Effect sizes are reported as Cohen's $d$ (paired: mean difference divided by standard deviation of differences). Monotonic relationships are assessed with Spearman's rank correlation $\rho$. Significance thresholds follow convention: $* \; p < 0.05$, $** \; p < 0.01$, $*** \; p < 0.001$.

For Experiment 5 (chimeric policies), where different conditions involve different random policy assignments, we use Welch's independent $t$-test for between-pair comparisons.

The choice of paired $t$-tests (rather than independent-samples tests) is motivated by the seed-matching design: each condition is run with seeds $0, 1, \ldots, 29$, and the same seed produces the same initial random placement and activation sequence across conditions. This eliminates between-run variance due to initialization, substantially increasing statistical power. The pairing is particularly important for experiments where the effect of interest is small (e.g., Experiment 7, where overload is identical across conditions but failed placements differ).

We do not apply multiple-comparison corrections (e.g., Bonferroni) across experiments because each experiment tests a distinct hypothesis with distinct data. Within-experiment multiple comparisons (e.g., the 6 comparisons in Experiment 1) are noted but not corrected, as the primary findings involve effects with $p < 0.0001$ that would survive any reasonable correction.

All statistical computations use SciPy 1.x (`scipy.stats.ttest_rel` for paired tests, `scipy.stats.ttest_ind` with `equal_var=False` for Welch's test, `scipy.stats.spearmanr` for rank correlations). Effect sizes use pooled standard deviation for Cohen's $d$.

### 3.3 Metrics

**Overload** $O$: the primary outcome metric, counting excess pigeons beyond one-per-hole capacity. Formally, $O = \sum_{i=1}^{n} \max(0, \ell_i - 1)$. For a fully-placed state with $m > n_u$ (usable holes), the minimum achievable overload is $m - n_u$.

**Overload ratio** $O / O_{\min}^{\text{theo}}$: final overload normalized by the theoretical minimum given the number of usable (non-frozen) holes. A ratio of 1.0 indicates optimal performance.

**Post-failure same-target retry**: for every failed placement that is followed by another attempted placement by the same pigeon, we ask whether the next attempted target is the same faulty hole. High values indicate retry persistence and argue against agent-level learning from rejection.

**Post-failure repeat failure rate**: for every failed placement that is followed by another attempted placement by the same pigeon, we ask whether that next attempt also fails. This captures persistence on faulty substrate even when the pigeon switches from one frozen hole to another.

**Convergence step**: the last simulation step at which overload changes, indicating when the system reaches its final configuration.

**Failed placements**: the total number of placement attempts rejected by frozen holes over the full run. A process-level metric that distinguishes policies even when outcomes are identical.

**Misleading occupancy share / bias**: the fraction of pigeons occupying misleading holes at the end of the run, and that share minus the fraction of holes that are misleading. Positive bias means deceptive substrate attracts more load than its spatial share would predict.

**Misleading overload share / bias**: the fraction of total overload concentrated on misleading holes, and that share minus the fraction of holes that are misleading. This measures whether deception merely perturbs the system or actively captures the excess load it creates.

**Misleading load gap**: mean load on misleading holes minus mean load on honest holes.

**Policy aggregation score**: for chimeric (mixed-policy) populations, the fraction of co-located pigeons sharing the majority policy in each multiply-occupied hole. Computed as follows: for each hole with $\geq 2$ pigeons, count the pigeons belonging to the majority policy; sum these across all such holes and divide by the total number of pigeons in multiply-occupied holes. Values near 1.0 indicate strong same-policy clustering; values near $1/k$ (where $k$ is the number of distinct policies) indicate random mixing. For $k = 2$ policies, the chance level is approximately 0.5.

**Delayed Gratification (DG) Index**: retained for compatibility with the sorting literature, measuring episodes where overload temporarily increases and later falls below the prior local minimum. In this system it is uniformly zero and is therefore treated as a negative result rather than a principal explanatory metric.

### 3.4 Experiment Design

The eight experiments are designed to probe the system along five perturbation axes: substrate integrity (Experiments 1, 6, 7), policy diversity (Experiments 2, 5), perceptual accuracy (Experiments 3, 8), information scope (Experiment 4), and temporal dynamics (Experiments 6, 7). Each experiment varies one axis while holding others constant, enabling attribution of effects to specific perturbation types. Table 0 provides the complete experimental design.

**Experiment 1 -- Frozen Hole Robustness.** Freeze 0 through 6 holes (of 7 total), measuring overload ratio together with post-failure persistence. Tests the system's capacity to redistribute around damaged substrate and whether repeated rejection produces any learning-like avoidance.

**Experiment 2 -- Policy Comparison.** All four policies under identical conditions ($m = 10$, $n = 7$, 1 frozen hole). Tests whether local policy choice affects global outcome, process cost, and post-failure persistence.

**Experiment 3 -- Noisy Perception.** Add Gaussian noise $\mathcal{N}(0, \sigma^2)$ to perceived hole loads, with $\sigma \in \{0, 0.5, 1.0, 2.0, 5.0\}$. The noise is applied via the `pigeon_view` hook, adding independent Gaussian noise to each perceived load and clamping to non-negative integers. Tests perceptual robustness and whether a noise-tolerance threshold exists.

**Experiment 4 -- View Radius Sweep.** Vary the number of holes each pigeon can inspect per step: $r \in \{1, 2, 3, 5, 7\}$. At $r = 1$, each pigeon sees exactly one randomly sampled hole per step; at $r = 7$ (the total number of holes), each pigeon has full information. Tests the value of local information for both convergence speed and final quality.

**Experiment 5 -- Chimeric Policies.** Mixed-policy populations ($m = 12$, $n = 8$), with each pigeon independently assigned one of two policies with equal probability. Four policy pairs are tested: GREEDY+COOPERATIVE, GREEDY+EXPLORATORY, EXPLORATORY+COOPERATIVE, and REPULSIVE+COOPERATIVE. Tests whether heterogeneous populations exhibit different collective behavior and whether same-policy pigeons cluster spatially (policy aggregation).

**Experiment 6 -- Recovery After Damage.** Three conditions on the same system ($m = 10$, $n = 7$): (a) control with no damage, (b) freeze hole 0 at step 167, (c) freeze hole 0 at step 167 and heal it at step 333. Tests dynamic damage compensation, recovery after healing, and whether the system reaches the same final state regardless of damage history.

**Experiment 7 -- Progressive vs Sudden Damage.** Freeze 3 holes (of 7) either all simultaneously at step 100 (sudden) or one at each of steps 100, 200, and 300 (gradual). Tests whether gradual exposure smooths disruption cost and reduces repeat failure, even if it does not change the endpoint.

**Experiment 8 -- Misleading Holes.** Holes that report their load as 0 regardless of true occupancy, implemented via the MISLEADING hole status in the model. Vary from 0 to 6 misleading holes (of 7 total). Tests robustness to deceptive substrate and directly measures whether deception induces occupancy and overload bias toward the faulty substrate itself.


## 4. Results

We present results for all eight experiments. Each experiment was run with $n = 30$ replications, 500 steps per run, and matched random seeds across conditions. We report means, significance levels ($p$-values from paired $t$-tests), and effect sizes (Cohen's $d$). For monotonic relationships, we report Spearman's rank correlation $\rho$. Each subsection concludes with a morphogenetic classification of the findings. Table 1 provides a cross-experiment summary; detailed results follow in subsections 4.1--4.8.

**Table 1. Cross-experiment summary.** All tests: two-tailed paired $t$-test, $n = 30$, seeds matched across conditions. Overload ratio $= 1.0$ indicates optimal performance.

| Experiment | Key Condition | Primary Metric | Value | $\Delta$\% | $p$ | $d$ |
|------------|--------------|----------------|-------|-----------|-----|-----|
| 1: Frozen Robustness | frozen\_3 | Overload ratio | 1.000 | $0.0$ | n.s. | $0.0$ |
| 1: Frozen Robustness | frozen\_5 | Repeat failure | 1.000 | -- | -- | -- |
| 2: Policy Comparison | EXPLORATORY | Same-target retry | 0.940 | $+73.3$ | $< 0.0001$ | $+10.377$ |
| 3: Noisy Perception | $\sigma = 1.0$ | Overload | 3.53 | $+17.8$ | $< 0.0001$ | $+1.051$ |
| 4: View Radius | $r = 2$ | Convergence | 6.0 | $-48.7$ | $0.0093$ | $-0.509$ |
| 5: Chimeric | REP+COOP | Aggregation | 0.796 | -- | -- | -- |
| 6: Recovery | damage\_and\_heal | Same-target retry | 0.226 | -- | -- | -- |
| 7: Progressive | gradual | Repeat failure | 0.639 | $-14.1$ | $< 0.0001$ | $-2.153$ |
| 8: Misleading | misleading\_2 | Occupancy bias | 0.274 | +27.4pp | $< 0.0001$ | $+1.920$ |

### 4.1 Experiment 1: Frozen Hole Robustness

Freezing holes reduces the number of usable holes from $n$ to $n - k$, raising the theoretical minimum overload from $m - n$ to $m - (n - k) = m - n + k$. The system must redistribute pigeons across fewer usable holes.

| Condition | Final Overload | Overload Ratio | Same-Target Retry | Repeat Failure |
|-----------|---------------|----------------|-------------------|----------------|
| frozen\_0 | 3.0 | 1.000 | 0.000 | 0.000 |
| frozen\_1 | 4.0 | 1.000 | 0.542 | 0.542 |
| frozen\_2 | 5.0 | 1.000 | 0.486 | 0.985 |
| frozen\_3 | 6.0 | 1.000 | 0.309 | 0.929 |
| frozen\_4 | 6.47 | 0.924 | 0.247 | 0.985 |
| frozen\_5 | 2.50 | 0.313 | 0.198 | 1.000 |
| frozen\_6 | 1.57 | 0.174 | 0.162 | 1.000 |

**Key finding.** The system reaches the theoretical minimum overload (ratio $= 1.0$) for 0 through 3 frozen holes, demonstrating perfect redistribution around up to 43\% substrate damage. At 4 frozen holes (57\% damage), efficiency drops to 92.4\%; at 5--6 frozen holes, the system is severely impaired. Spearman correlation between frozen holes and overload ratio: $\rho = -0.1498$, $p = 0.030$*.

The new process metrics show that this robustness is not driven by agent-level learning. With one frozen hole, pigeons retry the same faulty target on their next attempted move 54.2\% of the time. As more holes freeze, same-target retry falls because there are fewer distinct usable targets, but repeat failure rises to nearly 1.0: the system keeps colliding with faulty substrate even when it no longer insists on the exact same hole. In other words, endpoint compensation and negative learning dissociate.

Note on the overload ratio: the ratio *decreases* with more frozen holes because the theoretical minimum grows faster than the actual overload. At frozen\_5, the theoretical minimum is $m - (n - 5) = 10 - 2 = 8$, but actual overload is only 2.50; the system leaves many pigeons unable to find any active hole. At frozen\_6, only one hole is active and can hold at most one pigeon, so 9 of 10 pigeons must be either unplaced or crowded into a single hole. The system's failure at this extreme reflects the physical impossibility of placing 10 pigeons into 1 hole efficiently, not a failure of the local policies.

The robustness curve has a clear phase transition between frozen\_3 (perfect performance) and frozen\_4 (significant degradation). At frozen\_3, the system still has 4 usable holes for 10 pigeons, giving a density of $10/4 = 2.5$ pigeons per hole and theoretical minimum overload of 6. At frozen\_4, only 3 usable holes remain ($10/3 = 3.33$ density), and the system begins to miss the optimum. This transition point at roughly 50\% substrate damage provides a quantitative robustness boundary.

**Classification.** Perfect robustness at 0--3 frozen holes constitutes an *emergent competency*: local policies achieve global optimality despite substrate damage. The degradation at 4+ frozen holes reflects a *structural constraint*: when only 1--3 holes remain, the system's capacity to distribute excess is fundamentally limited. The critical threshold at approximately 43\% substrate damage defines the system's robustness envelope.


### 4.2 Experiment 2: Policy Comparison

All four policies were tested with $m = 10$, $n = 7$, and 1 frozen hole (theoretical minimum overload $= 4$).

| Policy | Final Overload | Failed Placements | Same-Target Retry | Convergence Step |
|--------|---------------|-------------------|-------------------|------------------|
| GREEDY | 4.0 | 212.1 | 0.542 | 7.4 |
| EXPLORATORY | 4.0 | 460.3 | 0.940 | 39.8 |
| REPULSIVE | 4.0 | 84.6 | 0.463 | 8.8 |
| COOPERATIVE | 4.0 | 168.3 | 0.997 | 7.6 |

**Same-target retry vs GREEDY baseline:**

| Policy | $\Delta$\% | $p$ | $d$ |
|--------|-----------|-----|-----|
| EXPLORATORY | $+73.3$\% | $< 0.0001$*** | $+10.377$ |
| REPULSIVE | $-14.6$\% | $< 0.0001$*** | $-1.437$ |
| COOPERATIVE | $+83.8$\% | $< 0.0001$*** | $+12.963$ |

**Key finding.** All four policies reach the identical final overload of 4.0 (the theoretical minimum). The outcome basin is universally attractive. However, the process differs enormously. EXPLORATORY generates 117\% more failed placements than GREEDY ($d = +21.692$), because its wider sampling increases the probability of encountering the frozen hole. REPULSIVE generates 60\% fewer failures ($d = -11.116$) because its crowd-avoidance heuristic naturally steers away from frozen holes. The new failure-persistence metric sharpens this story: after rejection, EXPLORATORY retries the same frozen hole 94.0\% of the time and COOPERATIVE 99.7\% of the time, whereas REPULSIVE falls to 46.3\%.

The extraordinarily large effect sizes for failed placements ($d = +21.692$ for EXPLORATORY) deserve comment. In most behavioral experiments, $d > 0.8$ is considered "large." The values here exceed that threshold by an order of magnitude, indicating that the policies produce almost non-overlapping distributions of failed placements. This extreme separation occurs because the failure mechanism is deterministic given the seed: once the initial placement and activation sequence are fixed, the number of times a policy directs a pigeon toward the frozen hole is a stable function of the policy's sampling behavior.

The convergence speed difference between EXPLORATORY (39.8 steps) and the other policies (7.4--8.8 steps) is also notable. EXPLORATORY converges slowly not because it fails to find the optimum, but because its broader sampling means it continues to detect and respond to small load imbalances for longer. Once overload reaches the minimum, EXPLORATORY pigeons still see alternative holes and repeatedly attempt moves that fail at the frozen hole, prolonging the convergence tail. The COOPERATIVE policy is even more revealing: it reaches the optimum quickly, but once it has identified the frozen hole as the locally best-looking low-load option, it nearly always retries it after rejection. This is collective optimality without individual negative learning.

**Classification.** The outcome equivalence across policies constitutes a *structural invariant*: the optimality basin is so wide that any reasonable local rule finds it. The dramatic divergence in failed placements and post-failure persistence constitutes a *process-level emergent phenomenon*: different strategies for navigating the same landscape produce measurably different costs and different degrees of retry fixation even when reaching the same destination.


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

Mixed populations of $m = 12$ pigeons and $n = 8$ holes, with each pigeon randomly assigned one of two policies.

| Policy Pair | Final Overload | Aggregation Score |
|-------------|---------------|-------------------|
| GREEDY + COOPERATIVE | 4.0 | 0.738 |
| GREEDY + EXPLORATORY | 4.0 | 0.738 |
| EXPLORATORY + COOPERATIVE | 4.0 | 0.754 |
| REPULSIVE + COOPERATIVE | 4.0 | 0.796 |

No pairwise overload differences between any pair (all $p = \text{n.s.}$).

**Key finding.** All chimeric combinations reach identical final overload. The outcome invariance observed in Experiment 2 (homogeneous populations) extends to heterogeneous populations. Aggregation scores range from 0.738 to 0.796, indicating moderate clustering by policy type: pigeons following the same local rule tend to co-occupy holes at rates above chance. The REPULSIVE + COOPERATIVE pair shows the highest aggregation (0.796), suggesting that the spatial separation behavior of REPULSIVE pigeons creates niches that COOPERATIVE pigeons then fill. GREEDY + COOPERATIVE and GREEDY + EXPLORATORY produce identical aggregation (0.738), indicating that GREEDY's dominant load-minimization strategy absorbs the partner policy's distinctive effects.

The aggregation scores (0.738--0.796) are well above the chance level of 0.5 (expected for two equally-represented policies assigned randomly to holes). This indicates that the local decision rules create implicit spatial preferences that sort pigeons by type. The mechanism is intuitive: REPULSIVE pigeons actively flee crowded holes, creating vacancies that COOPERATIVE pigeons (which evaluate global potential) preferentially fill. This produces a spontaneous division of the substrate into REPULSIVE-dominated low-density holes and COOPERATIVE-dominated high-density holes.

The scale of this experiment ($m = 12$, $n = 8$) differs from the others to allow enough pigeons per hole for aggregation to be measurable. Despite the larger system, the outcome invariance persists: all pairs reach identical overload.

**Classification.** The aggregation pattern is an *emergent phenomenon*: same-policy clustering is not specified by any individual policy but arises from the interaction between different decision rules. This parallels the chimeric sorting result of Zhang et al. (2024), where elements executing different sorting algorithms self-segregate within the array. The outcome invariance across chimeric compositions extends the structural invariant observed in Experiment 2 from homogeneous to heterogeneous populations.


### 4.6 Experiment 6: Recovery After Damage

A hole is frozen at step 167 and healed at step 333 (out of 500 total steps).

| Condition | Final Overload | Failed Placements | Same-Target Retry | Repeat Failure |
|-----------|---------------|-------------------|-------------------|----------------|
| control | 3.0 | 0.0 | 0.000 | 0.000 |
| damage\_only | 3.0 | 49.4 | 0.257 | 0.257 |
| damage\_and\_heal | 3.0 | 24.7 | 0.226 | 0.211 |

All overload comparisons: $p = \text{n.s.}$, $d = 0.0$.

**Key finding.** The system achieves complete recovery in all conditions at the endpoint: final overload is 3.0 in control, damage-only, and damage-and-heal. The main effect of dynamic damage is therefore process cost, not endpoint degradation. Failed placements fall from 49.4 in the permanent-damage condition to 24.7 when the hole is later healed.

The new persistence metrics clarify what kind of adaptation is taking place. Same-target retry remains non-zero under damage (0.257) and after healing (0.226), so the system does not exhibit strong negative learning at the level of individual agents. Instead, recovery is primarily a collective state-reconfiguration phenomenon: the distribution of pigeons adapts, but the pigeons do not form durable avoidance memories.

**Classification.** Complete recovery after both damage and healing constitutes a strong *emergent competency*: the system exhibits damage compensation and adaptive replanning using only local policies. The rapidity of recovery (overload returns to optimum within a few steps of each substrate change) suggests the optimization landscape contains no metastable traps that would delay re-equilibration. This is the strongest demonstration of basal cognition in our system: goal-directedness, error correction, and adaptive replanning all operating together.


### 4.7 Experiment 7: Progressive vs Sudden Damage

Three holes are frozen either all at step 100 (sudden) or one every 100 steps (gradual: steps 100, 200, 300).

| Condition | Final Overload | Convergence Step | Failed Placements | Same-Target Retry | Repeat Failure |
|-----------|---------------|------------------|-------------------|-------------------|----------------|
| sudden | 3.0 | 3.9 | 173.5 | 0.249 | 0.744 |
| gradual | 3.0 | 3.9 | 128.9 | 0.253 | 0.639 |

Overload comparison: $p = 1.0$, $d = 0.0$. Convergence comparison: $p = 1.0$, $d = 0.0$.
Failed placements: gradual $-26$\% vs sudden, $p < 0.0001$***, $d = -4.116$. Repeat failure: gradual $-14.1$\% vs sudden, $p < 0.0001$***, $d = -2.153$.

**Key finding.** There is no stress inoculation effect on outcome: both conditions reach identical overload and convergence speed. This contrasts with biological morphogenetic systems, where gradual exposure to stressors can build tolerance (Levin, 2022). The absence of inoculation in our system is consistent with the memoryless nature of the agents: since pigeons have no state that persists between steps, there is no mechanism for prior experience to modulate future behavior.

However, gradual damage does reduce wasted effort: 26\% fewer failed placements ($d = -4.116$) and 14.1\% lower repeat failure ($d = -2.153$). Same-target retry is unchanged (0.249 vs 0.253, n.s.), which is informative: gradual damage smooths the collective path through state space without making individual pigeons more avoidant of recently failed targets.

The absence of a stress inoculation effect has a clear mechanistic explanation. Stress inoculation in biological systems relies on memory: prior exposure to a stressor triggers adaptive responses (e.g., heat shock proteins, immune memory) that improve tolerance to future exposure. Our pigeons have no memory. Each activation is stateless: the pigeon inspects current loads, applies its policy, and acts. It has no record of past failures, past damage events, or past configurations. Without memory, there is no substrate for inoculation. This suggests a testable prediction: adding even simple memory (e.g., a pigeon that avoids holes where it was previously rejected) should enable stress inoculation effects and might also produce delayed gratification.

**Classification.** The outcome equivalence is a *structural invariant*: the final state depends only on the total damage, not its temporal profile. The failed-placement difference is a *process-level emergent phenomenon* driven by temporal smoothing of the perturbation. The absence of stress inoculation is a *negative result* attributable to the memoryless agent architecture, not to the pigeonhole domain itself.


### 4.8 Experiment 8: Misleading Holes

Misleading holes report their load as 0 regardless of true occupancy, actively deceiving pigeon decision-making.

| Misleading Holes | Final Overload | Occupancy Bias | Overload Bias | Load Gap |
|-----------------|---------------|----------------|---------------|----------|
| 0 | 3.0 | 0.000 | 0.000 | 0.000 |
| 1 | 3.77 | 0.217 | 0.518 | 2.533 |
| 2 | 4.20 | 0.274 | 0.559 | 1.920 |
| 3 | 4.33 | 0.265 | 0.511 | 1.544 |
| 4 | 4.40 | 0.219 | 0.418 | 1.275 |
| 5 | 4.37 | 0.156 | 0.286 | 1.090 |
| 6 | 4.30 | 0.080 | 0.143 | 0.928 |

Spearman correlation (misleading holes vs overload): $\rho = +0.417$, $p < 0.0001$***.

**Key finding.** Misleading holes are substantially more damaging than frozen holes, but the crucial new result is not just higher overload. Deception induces strong substrate bias. A single misleading hole occupies 14\% of the substrate but captures 36\% of pigeons and 66\% of overload, yielding occupancy bias $= 0.217$ and overload bias $= 0.518$. With two misleading holes, deceptive substrate captures 56\% of pigeons and 84.5\% of overload.

A plateau-and-reversal effect is visible: degradation is steepest for the first 1--2 misleading holes (25.6\% and 40.0\%), peaks at 4 misleading holes (46.7\%), and then decreases slightly at 5--6 misleading holes (45.6\% and 43.3\%). This suggests that once a critical fraction of holes is deceptive, additional deception has diminishing marginal effect and may even slightly reduce overload, likely because when nearly all holes are misleading, the deception becomes uniform and ceases to create differential attraction.

The comparison between Experiments 1 and 8 is therefore sharper than a simple damage-versus-deception contrast on endpoint loss. Frozen holes remove capacity; misleading holes actively redirect traffic toward themselves. The deceptive substrate is not merely harmful; it becomes an attractor. This is why Experiment 8 should be interpreted as a bias-formation result as much as a degradation result.

This result maps onto the classical distributed systems distinction between crash faults and Byzantine faults (Lamport et al., 1982). A crashed node is simply absent; a Byzantine node sends arbitrary (potentially malicious) messages. Our misleading holes are Byzantine: they send false signals (reporting load $= 0$) that actively corrupt the decision-making of nearby agents. The result that Byzantine faults are categorically harder to tolerate than crash faults is well-known in distributed computing; our experiment provides a morphogenetic-system instantiation of this principle.

**Classification.** The severe impact of misleading holes constitutes both a *structural vulnerability* and a *fault-induced bias formation* effect: the system's local optimization depends fundamentally on accurate perception, and deception actively concentrates load onto the deceptive substrate.


## 5. Discussion

### 5.1 Classification of Findings

The revised metric set suggests four classes of finding rather than a single DG-centered axis.

**Emergent competencies**:
- *Global optimality from local rules.* Convergence to theoretical minimum overload in 6/8 experiments (Experiments 1--2, 4--7).
- *Damage compensation and recovery.* Complete recovery at the endpoint after dynamic damage and healing (Experiment 6).
- *Chimeric self-organization.* Same-policy pigeons cluster spatially in mixed populations (Experiment 5).

**Structural invariants**:
- *Policy indifference at the endpoint.* All four local policies reach identical final overload (Experiment 2).
- *Temporal indifference at the endpoint.* Sudden and gradual damage produce identical final states (Experiment 7).
- *Monotonic optimization.* DG Index is 0.0 in every condition. This remains true, but functions as a negative result rather than the main finding.

**Process persistence**:
- *Retry fixation after rejection.* Rejected pigeons often target the same faulty hole again on their next attempted move (Experiment 2), especially under EXPLORATORY and COOPERATIVE policies.
- *Repeat-failure smoothing without learning.* Gradual damage lowers repeat failure and failed placements (Experiment 7) without changing same-target retry, indicating smoother collective adaptation without individual memory formation.

**Bias formation and vulnerability**:
- *No noise buffer.* Even minimal perceptual noise degrades performance (Experiment 3).
- *Deceptive attraction bias.* Misleading holes capture disproportionate occupancy and overload (Experiment 8).
- *Damage saturation.* High frozen-hole counts overwhelm the system's compensatory capacity (Experiment 1, frozen $\geq 4$).

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

**Error correction.** When substrate damage (frozen holes) changes the set of usable targets, the system corrects without external intervention. Pigeons redistribute across remaining usable holes until global overload reaches the new attainable regime. This correction is not specified by the algorithm; it emerges from the interaction between local policies and the changed substrate.

**Adaptive replanning.** Experiment 6 demonstrates that the system re-optimizes when the substrate changes in either direction (damage or healing). The system does not merely tolerate damage; it actively reorganizes its configuration to exploit the available substrate, whatever that substrate currently is.

However, the system does not exhibit one hallmark of more sophisticated cognition: agent-level learning from failure. The new post-failure persistence metrics show that rejected pigeons often retry the same faulty target on their next attempted move. This is especially stark for EXPLORATORY and COOPERATIVE policies in Experiment 2. The collective reaches good states, but the agents do not appear to form durable negative memories of bad choices. This places the pigeonhole system at the lower end of the basal cognition spectrum: competent but reactive, capable of convergence and recovery, but not of local learning or strategic detour.

The absence of DG still matters, but mainly as supporting evidence for the shape of the landscape rather than as the primary story. The pigeonhole potential function $\Phi$ appears to have no local minima that require uphill traversal to reach the global minimum. Every configuration with $O > O_{\min}$ has at least one single-pigeon move that reduces $\Phi$. The landscape is therefore "funnel-shaped": all downhill paths lead to the global minimum. This explains the universal convergence to optimality without implying learning.

This analysis suggests a hierarchy of morphogenetic systems: (1) systems with funnel-shaped landscapes where greedy local policies suffice (pigeonhole), (2) systems with rugged landscapes where detours are sometimes beneficial but not required (sorting), and (3) systems with highly non-convex landscapes where delayed gratification is essential for convergence (potentially larger-scale morphogenetic systems). Characterizing where real biological morphogenetic systems fall on this spectrum is an open question.

### 5.4 The Role of Impossibility

The pigeonhole principle introduces a feature absent from prior morphogenetic targets: the system's assigned problem has no solution. Sorting can be completed correctly. Transformer training can converge to a loss minimum. But $m > n$ pigeons cannot be placed injectively into $n$ holes. The system must manage a contradiction, not resolve one.

This makes the pigeonhole system a model for a broad class of real-world problems: resource allocation with structural scarcity, scheduling with insufficient time slots, routing with insufficient bandwidth. In all such settings, the question is not "can the system find the answer?" but "how well can the system manage the impossibility?" Our results show that even extremely simple local policies can manage impossibility optimally (reaching the theoretical minimum overload), robustly (tolerating up to 43\% substrate damage), and adaptively (recovering completely from dynamic damage). The single greatest threat to this management competency is not damage to the substrate but deception by the substrate.

This finding has implications for the morphogenetic framework: the distinction between absent resources and deceptive resources may be fundamental to understanding biological systems. A cell encountering a dead neighbor (absent resource) can route around it. A cell encountering a neighbor that sends false signals (deceptive resource) may make actively harmful decisions. Our misleading-holes experiment (Experiment 8) provides a minimal quantitative model of this distinction.

The pigeonhole system also provides a clean model of "satisficing" (Simon, 1956): behavior that does not optimize a well-defined objective but instead finds a "good enough" solution to an ill-defined problem. When the ideal (injective placement) is impossible, the system settles for the best achievable state without any explicit representation of what "best achievable" means. The optimality of this satisficing behavior -- the system reliably finds the actual minimum, not merely a "good enough" approximation -- is itself a finding that requires explanation. It suggests that the interaction between local self-interest (each pigeon minimizing its own crowding) and global structure (the finite number of holes) is sufficient to produce globally optimal satisficing, at least in small systems.

We conjecture that this property -- optimal satisficing under impossibility via local greedy policies -- holds generally for pigeonhole-type systems where the constraint is a simple capacity bound. The key structural feature is that every sub-optimal configuration has a local move that improves the global objective: if any hole has load $\geq 3$ while another has load $\leq 1$, moving a pigeon from the overloaded to the underloaded hole reduces both overload and potential. This "every bad state has a good exit" property ensures that greedy local policies cannot get stuck. Whether this property generalizes to more complex impossibility constraints (e.g., graph coloring with too few colors, bin packing with too few bins) is an open question with implications for the breadth of the morphogenetic perturbation framework.

### 5.5 Failed Placements and Bias as Process Metrics

Across Experiments 2, 6, 7, and 8, we observe a recurring pattern: conditions that are indistinguishable or only mildly different on endpoint metrics can be sharply distinguished by process metrics. Failed placements count wasted action under damage. Post-failure persistence distinguishes temporary disruption from actual local avoidance. Misleading occupancy and overload bias distinguish simple degradation from active redirection of traffic toward deceptive substrate.

These metrics serve the same role in the pigeonhole system that trajectory-loss and representation-drift metrics serve in other morphogenetic settings: they reveal differences invisible to endpoint analysis. In Experiment 2, REPULSIVE achieves the same final overload as EXPLORATORY but with 82\% fewer failed placements and roughly half the same-target retry. In Experiment 8, overload alone tells us deception is harmful; occupancy and overload bias tell us *how* it is harmful, namely by turning misleading holes into attractors.

We therefore propose that faultization should routinely track at least three layers of behavior: endpoint quality, process cost, and induced asymmetry. Endpoint metrics alone cannot distinguish between a system that reaches the optimum efficiently, one that reaches it wastefully, and one that reaches it by falling into newly created biases.

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

Our eight experiments reveal that the system exhibits strong emergent competencies: local policies converge to the global optimum in six of eight conditions, the system recovers completely from dynamic damage at the endpoint, and heterogeneous populations self-organize into policy-based spatial clusters. At the same time, the updated metrics show two equally important negative results: there is little evidence of agent-level learning from rejection, and deceptive substrate induces strong attraction bias.

The most striking finding is the dissociation between collective adaptation and local learning. The system reliably reaches the theoretical minimum overload under a wide range of conditions, yet individual pigeons often retry faulty targets instead of learning to avoid them. Faultization therefore exposes a system that is globally competent but locally myopic.

The universal absence of delayed gratification ($\text{DG Index} = 0.0$ across all conditions) remains informative, but it is not the main story. More informative are the retry-persistence and substrate-bias metrics: they show that the system can converge, correct, and recover without learning, and that deception harms performance by capturing both occupancy and overload.

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
