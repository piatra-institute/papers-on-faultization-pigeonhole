# On Faultization: Pigeonhole

Morphogenetic perturbation of the pigeonhole principle, applying Levin et al.'s (2024) methodology to a distributed multi-agent system.

## Overview

The classical pigeonhole principle states that if m > n pigeons are placed into n holes, at least one hole must contain more than one pigeon. We reinterpret this impossibility theorem as a dynamical system: each pigeon is an autonomous agent with a local policy, each hole is a stateful resource, and the system self-organizes around the irreducible constraint (overload >= m - n).

Eight experiments systematically perturb the system -- freezing holes, corrupting perception, restricting visibility, mixing policies, damaging and healing substrate -- to reveal emergent competencies not prescribed by the local rules.

## Key Findings

- **Complete optimization**: Local policies reach theoretical minimum overload in 6 of 8 experiments
- **Policy indifference**: All four policies achieve identical outcomes but differ dramatically in process (failed placements vary by 5x)
- **No noise buffer**: Unlike transformer training, perceptual noise causes immediate monotonic degradation
- **Deceptive substrate is most damaging**: Misleading holes (+25-47% overload) are far worse than frozen holes (managed optimally up to 3)
- **Complete recovery**: System rapidly re-optimizes after both damage and healing events

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
