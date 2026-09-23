---
title: "On Faultization: Coverage and Failure in a Pigeonhole Model"
author: PIATRA . INSTITUTE
date: "March 2026 (revised September 2026)"
bibliography: references.json
link-citations: true
---

```{=latex}
\makeatletter
\def\fps@figure{!htb}
\makeatother
```

## Abstract

Load-seeking allocation rules can be drawn toward a resource that refuses entry, because a closed resource reports the lowest load. We study this failure in a small allocation model in which ten items move among seven holes using sampled load reports. The pigeonhole bound constrains fully placed assignments, but the usual overload measure records coverage and says nothing about balance, and it improves when items become unplaced. A paired audit separates placement, coverage and balance, gives every condition the same random inputs, and compares load-seeking rules with random movement, staying put, and an arrival-aware comparison. Across thirty seed tapes, closing five holes leaves a mean of 5.03 items unplaced under the original comparison rule. Sampling every hole does not help, whereas trying another candidate after rejection places every item. The effect of tiny Gaussian errors depends on how noisy loads are encoded: truncation and unquantized reports both worsen allocation, while nearest-integer rounding preserves the noiseless result at the smallest tested scale. Accounting for the arriving item prevents that endpoint loss, although movement continues. Blocking entry to a hole preserves its existing occupancy, whereas eviction creates a separate recovery problem. The failures lie in admission information and in local cost comparisons. The results support a method for inspecting perturbation models and license no further inference about cognition or access to mathematical patterns.

## Introduction

A hole reports zero occupants. An unplaced item chooses it and is refused entry. On a later activation, the same hole may again be the least crowded candidate, since its load report does not record the refusal. The item can keep making a locally reasonable choice without ever obtaining a place.

This is the central difficulty in the model. Each accepting hole has unlimited capacity, so closing some holes need not make placement impossible; it changes what a load-seeking rule can discover and use. The distinction matters when a simulation is described as tolerating a percentage of resource loss, because a low overload score may mean that work was never admitted.

We use *faultization* to mean deliberately disturbing a model's operating assumptions and inspecting what follows. The motivation comes in part from experiments on sorting arrays whose elements act locally and can be damaged [@zhang2025]. Levin's proposed relation between physical systems and mathematical patterns supplies a broader philosophical motivation [@levin2026]. Neither supplies an alternative transition rule for this allocation model, so the experimental question is which details of the rule account for its successes and failures.

The September audit replaces an earlier eight-experiment analysis of the same model. It retains the core placement model and preserves the old results, but uses new random inputs, narrower comparisons and separate measures of placement, coverage and balance. Its contribution is an account of failure mechanisms in a transparent toy system.

## Model and Outcome Measures

Let $m$ labeled items occupy $n$ labeled holes, with unplaced items permitted. Write $\ell_i$ for a hole's true load, $U$ for the number unplaced, $P=m-U$ for the number placed and $H$ for the number of occupied holes. The original overload measure satisfies the identity

$$
O=\sum_i\max(0,\ell_i-1)=P-H.
$$

For a fully placed assignment with $m>n$, the pigeonhole bound is $O\geq m-n$. Equality means every hole is occupied and says nothing about how the remaining items are distributed. In the present system the loads $(2,2,2,1,1,1,1)$ and $(4,1,1,1,1,1,1)$ both have overload $3$. Their sums of squared loads, $Q=\sum_i\ell_i^2$, are $16$ and $22$ respectively, so $Q$ distinguishes their concentration.

With $k$ accepting holes, all items placed and none retained in a closed hole, write $m=kq+r$, with $0\leq r<k$. The minimum squared load is

$$
Q_*=(k-r)q^2+r(q+1)^2.
$$

Moving an item between two loads differing by more than one reduces $Q$ until only these adjacent load sizes remain. We report balance regret $Q-Q_*$ only under those placement conditions. In other states, $U$, occupied accepting holes and occupied closed holes are kept as separate outcomes, since combining them into a single penalty would require a choice about their relative importance.

The model is small enough for direct checks. Enumeration of 8,008 load vectors confirms a minimum $Q$ of 16 for ten items and seven open holes. Among the 282,475,249 fully placed labeled assignments, 29,635,200 cover every hole and 15,876,000 are balanced. Independent uniform placement therefore starts with complete coverage with probability 0.1049 and balance with probability 0.0562. Improvement on these starting rates is a measurable property of a policy; the bound alone does not produce it.

Two local comparisons need to be distinguished. Suppose an item currently shares a hole of load $a$ and considers a different hole of load $b$. After moving, its new load is $b+1$, and

$$
\Delta Q=(a-1)^2+(b+1)^2-a^2-b^2=2(b-a+1).
$$

The original greedy comparison accepts $b<a$. With truthful integer loads it cannot raise $Q$, but it permits neutral moves when $b=a-1$. Our arrival-aware alternative requires $b+1<a$ and therefore makes only strict improvements under the same conditions. The comparison is a special case of the cost accounting in congestion games, where the arriving player contributes to congestion [@rosenthal1973]. For this unrestricted, identical-resource, linear-load case, an unbalanced allocation always offers an improving move, and larger system size alone does not create suboptimal local minima of this cost.

## Audit Design

The audit uses ten items, seven holes and 500 sequential activations per run. Thirty independent seed tapes, numbered 6000–6029, determine initialization, activated items, ordered candidate samples and Gaussian errors through separate random streams. Conditions within a seed receive the same tapes. The separation of streams matters because two policies given the same seed do not keep matched activation sequences if they consume different numbers of random draws.

The usual start gives each item a uniformly selected hole; a second proposal is tried only if the first is closed, and two refusals leave the item unplaced. Healthy controls also start with every item in the same hole. Dynamic experiments start balanced. A closed hole rejects entry and reports its true occupancy, while a misleading hole admits items and always reports zero. Neither status is announced separately to the deciding item.

At each activation the load-seeking rules inspect three distinct holes sampled uniformly without replacement. "Radius" denotes this sample count and has no spatial meaning. The item's current hole is excluded as a relocation destination, and its current load is known exactly. The greedy rule picks the lowest reported destination load below that current load. The arrival-aware rule adds the arriving item before comparing. An unplaced item regards its current cost as infinite. Ties follow the common sampled order, and a rejected move leaves an existing assignment intact.

Two null policies show what the load observations contribute: staying put, and selecting a uniform destination without inspecting its load. A separate retry control proceeds to the next eligible candidate in the same sample after a rejection. It has no memory between activations but may spend more admission attempts. Load-based rules pay for each sampled report, and the nulls make no load queries. The accounting does not treat an observation and an attempted admission as having identical computational costs.

The full design has 32 conditions, varying static closures, sample count, retry, noisy-load encoding, misleading reports and close-versus-evict events. In the earlier analysis, the extra probes of the exploratory policy read true loads and the cooperative policy consulted the true global potential. Those are different information privileges, so the audit does not compare them with local readers of the same faulty reports.

The design and twelve primary paired contrasts were written down before the new outcomes were examined. The audit is exploratory, informed by the earlier analysis and code, and was not preregistered. Reported intervals are pointwise 95% paired $t$ intervals across seed tapes. Holm adjustment applies to the twelve tests as one family and leaves the intervals unadjusted [@holm1979]. Identical observed differences produce degenerate sample intervals, which do not establish population equivalence. Other summaries are descriptive.

We record first coverage, first balance, final state, rejected attempts and actual assignment changes. An event that never occurs has a missing, censored time. The last change in overload is recorded under that name and is not called convergence, because a balanced allocation and a motionless system are different endpoints.

## Healthy Runs and Closed Holes

With all holes open, both load-seeking rules finish balanced in every run, from both uniform and concentrated starts. Random movement also visits coverage and balance in every run, but its final mean squared load is 22.33, compared with 16.00 for greedy. The paired excess is 6.33, with interval [4.83, 7.84], from either start; reaching a state once is weak evidence that a process maintains it. Staying put retains mean squared loads of 23.13 from uniform starts and 100.00 from concentrated starts.

The healthy greedy rule's overload stops changing after a mean of 4.17 activations from uniform starts, but its last assignment change occurs at a mean of 499.17. It makes another 288.07 moves, on average, after first achieving coverage. The arrival-aware rule finishes with the same balanced load vector, up to permutation, and its last move occurs at a mean of 5.67. The neutral moves allowed by the pre-arrival comparison account for the difference.

Static closure exposes a more consequential error. With five holes closed and a three-hole sample, the mean final unplaced count is 5.03. Both accepting holes are occupied in every run, yet no run places all items. The mean overload is 2.97, below the fully placed seven-hole minimum, and the apparent improvement reflects items that were never placed.

Once the two accepting holes are occupied, every three-hole sample includes an empty closed hole. That hole reports zero while every accepting hole reports a positive load, so the greedy rule selects a refusal. The state is absorbing for the placement dynamics even though the remaining holes have spare capacity; each could hold all the items. The argument applies whenever all accepting holes are occupied and their number is smaller than the sample count.

![Admission and coverage at the end of the five-closure runs. Bars show means over thirty paired tapes. Three- and seven-hole samples leave 5.03 items unplaced; one-hole sampling and within-activation retry leave none. All four conditions occupy both accepting holes. Retry uses a three-hole sample.](../simulation/output/september-audit/admission.png){width=100%}

Inspecting all seven holes yields the same final unplaced count as inspecting three, on every tape. Inspecting only one allows placement to finish in every run, because an accepting destination can then be sampled without a closed competitor. Within-activation retry also places every item. Its paired reduction in unplaced count is 5.03, with interval [4.45, 5.62]. The retry control spends a mean of 1083.53 admission attempts against 500.00 without retry, so the additional progress has an explicit cost.

Additional observations help only when the decision rule can use them. The classical balanced-allocation results study the benefit of choosing among sampled loads, in both sequential and removal/replacement settings [@azar1999]. The present finite system adds relocation and rejecting destinations, samples without replacement, and measures different endpoints, so the closure result is no counterexample to those theorems. It shows that their favorable intuition cannot be carried over without checking what a candidate load reveals about admission.

## Noisy and Misleading Load Reports

The original noise operator is \texttt{max(0, int(load + noise))}. It truncates toward zero and clips negative results, which differs from rounding to the nearest integer. A load of $2-10^{-6}$ becomes $1$, while $2+10^{-6}$ remains $2$, so an arbitrarily small negative error can lower a positive integer report by a whole unit.

We compare this encoding with nearest-integer rounding followed by clipping, and with signed unquantized reports. The current occupied load remains exact in every variant. At noise standard deviation $10^{-6}$, the greedy rule's final mean $Q$ rises from 16.00 to 17.60 with truncation. The paired increase is 1.60 [0.81, 2.39], with Holm-adjusted $p=0.0023$. Nearest-integer rounding reproduces the noiseless result at this scale.

Truncation is only part of the explanation. Unquantized tiny noise gives mean $Q=17.47$, an increase of 1.47 [0.73, 2.20], also with adjusted $p=0.0023$. Two truly equal loads lie on the greedy rule's decision boundary: a slightly underestimated destination becomes eligible, even though the arriving item makes it more crowded. Removing integer conversion leaves that comparison intact.

![Mean final squared load under three report encodings and two comparison rules. All conditions use thirty paired tapes. The horizontal axis spaces the three tested noise scales categorically; connecting lines do not estimate an intervening response curve. The reference line is the balanced value, 16.](../simulation/output/september-audit/noise.png){width=100%}

The arrival-aware rule finishes at $Q=16$ in every tiny-noise condition. The result concerns the endpoint, and the noisy trajectories do change: with tiny truncated noise the rule's last move occurs at a mean of 498.33 activations, against 5.67 without noise. An underestimate smaller than one unit can admit a truly neutral move under the stricter comparison, but it cannot admit a harmful one.

```{=latex}
\begin{samepage}
```

At standard deviation 0.5, greedy truncation exceeds rounding by 0.80 in mean $Q$, with interval [0.13, 1.47]. The adjusted $p$ is 0.103, so this contrast does not clear the familywise threshold of 0.05. These scales do not establish a general noise-tolerance curve. They isolate a conversion discontinuity and a decision boundary that the earlier description of "discrete fidelity" obscured.

```{=latex}
\end{samepage}
```

A permanently misleading hole produces a further separation between outcomes:

| Rule | Honest overload | Misleading overload | Honest squared load | Misleading squared load |
|:--|--:|--:|--:|--:|
| Greedy | 3.00 | 3.60 | 16.00 | 20.47 |
| Arrival-aware | 3.00 | 3.00 | 16.00 | 17.00 |

Table 1. Means at the final activation, with one accepting hole reporting zero in the misleading conditions. Each row compares thirty paired tapes.

For greedy, the overload increase is 0.60 [0.31, 0.89]. Arrival-aware preserves full coverage in every run, but its squared-load increase is 1.00 [0.39, 1.61], with adjusted $p=0.0139$. A coverage-only assessment would miss this concentration cost. Neither rule verifies the reported occupancy, and the arrival-aware correction is insufficient against a persistent false report.

## Closure, Eviction and Recovery

For the dynamic comparison, one hole closes after activation 100 and reopens after activation 300. Blocking entry alone keeps its occupants. In these runs the assignment remains fully placed and the overload stays at 3 throughout. Attempts are rejected during closure, but no coverage is lost, and describing the unchanged endpoint as rapid recovery would credit the system with replacing occupancy that was never removed.

Eviction changes the experiment. At closure the affected items become unplaced, with a mean count of 1.50, while overload falls from 3.00 to 2.50; again a lower overload accompanies a worse placement state. Every run replaces its evicted items before reopening, with a mean latency of 21.57 activations. Immediately before reopening, all items occupy the six accepting holes and overload is 4. Reopening moves no item by itself; full seven-hole coverage returns after a further mean of 2.73 activations.

The distinction also limits claims about learning from damage. Items have no persistent internal memory, but the collective assignment is state and can carry the effects of earlier events. A lasting benefit from prior damage would require a matched later challenge and a specified benefit, and the present experiment provides neither. Likewise, a trajectory that temporarily worsens a score does not demonstrate that the detour was necessary or that an item deferred a reward.

## Limitations

These conclusions concern one small allocation model. There are no service times, finite per-hole capacities, geometric neighborhoods, strategic reporters or evolving policies, and a larger empirical study would be needed to assess how the effects change across those choices. The exact overload identity, move-cost calculation and closed-hole trap have wider algebraic scope, but the reported effect sizes and completion times do not.

## Conclusion

A load report states how crowded a destination appears. It need not state whether entry is possible or what the load will be after arrival. Perturbation experiments become informative when these questions are separated and the resulting failures are counted: in this model, closed holes trap a greedy rule through their zero reports, small noise shifts outcomes through the encoding and the pre-arrival comparison, and a false zero report concentrates load even under the arrival-aware rule. How competent the system appears depends on which of these questions the evaluation measures.

## Reproduction

The repository contains the new protocol, paired-tape runner, raw per-run results, figures and a hash-bound execution record. The recorded run passed 26 regression tests and the mathematical checks. Python 3.12.4, NumPy 2.0.2, SciPy 1.14.1 and Matplotlib 3.9.2 were used; no external dataset is required. From \texttt{simulation/}, run \texttt{uv run --script audit.py --output output/my-audit}. The runner refuses to overwrite an existing result file or to write into the legacy results directory. The eight experiments of the earlier analysis remain available as historical material and are not the evidence for the revised numerical claims.

```{=latex}
\clearpage
```

## References
