# On Faultization: Pigeonhole

Morphogenetic perturbation of the pigeonhole principle, applying Levin et al.'s (2024) methodology to a distributed multi-agent system.

## Overview

The classical pigeonhole principle states that if m > n pigeons are placed into n holes, at least one hole must contain more than one pigeon. Under the Platonic Space framing (Levin, 2026), we treat the pigeonhole principle not as a rule the agents compute but as a pattern they channel from the latent mathematical structure: the optimal allocation (O_min = m-n) exists in the space of mathematical truths, and the agent-substrate system serves as an interface through which that pattern manifests.

Each pigeon is an autonomous agent with a local policy, each hole is a stateful resource, and the system self-organizes around the irreducible constraint -- not because any agent knows the global optimum, but because the pattern is robustly accessible through the local interface.

Eight experiments systematically perturb this interface -- narrowing bandwidth (frozen holes), blurring the sensory channel (noise), restricting information geometry (view radius), diversifying the interface type (policy mixtures), breaking and restoring it (recovery), and actively corrupting it (misleading holes) -- to probe the conditions under which the pigeonhole pattern manifests, degrades, or inverts.

## Key Findings

- **Pattern manifestation (free lunch)**: The pigeonhole pattern manifests fully in 6 of 8 experiments -- the system receives optimal allocation without computing it
- **Pattern plurality**: All four policies channel the same pattern with identical fidelity, but differ dramatically in process cost (failed placements vary by 5x, same-target retry from 0.46 to 1.00)
- **Pattern fidelity (discrete)**: Unlike transformer training, perceptual noise causes immediate monotonic degradation -- the interface tolerates zero corruption
- **No convincing agent-level learning**: Rejected pigeons often retry faulty substrate instead of learning to avoid it; the system is pattern-driven, not memory-driven
- **Pattern corruption**: A single misleading hole inverts the pattern, attracting 36% of pigeons and 66% of overload while raising overload by 25.6%
- **Bidirectional interface**: The collective state re-accesses the pattern after damage and healing with no hysteresis

## Quick Start

```bash
# Smoke test
uv run --script run.py test

# Run all experiments
uv run --script run.py all

# Statistical analysis
uv run --script analyze_stats.py all

# Generate plots
uv run --script visualize.py
```

## Project Structure

```
on-faultization-pigeonhole/
├── run.py                    # CLI entry point
├── model.py                  # Core pigeonhole system
├── experiments.py            # 8 experiments
├── perturbations.py          # Perturbation hooks
├── metrics.py                # Statistical metrics
├── visualize.py              # Plotting
├── analyze_stats.py          # Paired t-tests
├── CLAUDE.md                 # Quick reference
├── README.md
├── docs/
│   ├── PAPER.md              # Full research paper
│   ├── FINDINGS.md           # Detailed results
│   └── EXPERIMENTS.md        # Concise summary
├── scripts/
│   └── build-paper.sh        # PDF generation
├── results/                  # JSON + PNG outputs
└── data/                     # Reference papers
```

## Documentation

- [Paper](docs/PAPER.md) -- Full research paper with methodology and results
- [Findings](docs/FINDINGS.md) -- Detailed per-experiment results with p-values
- [Experiments](docs/EXPERIMENTS.md) -- Concise experiment summary

## References

Levin, M. (2026). The Platonic Space framework for morphogenetic competency.

Levin, M., Bongard, J., & Bhatt, R. (2024). Morphogenetic competencies of sorting algorithms. arXiv:2401.05375.
