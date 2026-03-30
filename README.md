# On Faultization: Pigeonhole

Morphogenetic perturbation of the pigeonhole principle, applying Levin et al.'s (2024) methodology to a distributed multi-agent system.

## Overview

The classical pigeonhole principle states that if m > n pigeons are placed into n holes, at least one hole must contain more than one pigeon. We reinterpret this impossibility theorem as a dynamical system: each pigeon is an autonomous agent with a local policy, each hole is a stateful resource, and the system self-organizes around the irreducible constraint (overload >= m - n).

Eight experiments systematically perturb the system -- freezing holes, corrupting perception, restricting visibility, mixing policies, damaging and healing substrate -- to reveal emergent competencies, retry persistence, and fault-induced bias not prescribed by the local rules.

## Key Findings

- **Complete optimization**: Local policies reach theoretical minimum overload in 6 of 8 experiments
- **Policy indifference with process divergence**: All four policies achieve identical outcomes but differ dramatically in process (failed placements vary by 5x, same-target retry from 0.46 to 1.00)
- **No noise buffer**: Unlike transformer training, perceptual noise causes immediate monotonic degradation
- **No convincing agent-level learning**: Rejected pigeons often retry faulty substrate instead of learning to avoid it
- **Deceptive substrate induces bias**: A single misleading hole attracts 36% of pigeons and 66% of overload while raising overload by 25.6%
- **Complete recovery**: The collective state re-optimizes after damage and healing even though retry persistence remains non-zero

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

Levin, M., Bongard, J., & Bhatt, R. (2024). Morphogenetic competencies of sorting algorithms. arXiv:2401.05375.
