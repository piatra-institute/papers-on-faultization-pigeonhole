# Faultized Pigeonhole

Morphogenetic perturbation experiments on a pigeonhole placement system.

## Running commands

Always use `uv run --script` to execute scripts:

```
uv run --script run.py <command> [--num-reps N] [--num-steps N] [--result-suffix SUFFIX]
```

## Key commands

```
uv run --script run.py test              # Quick smoke test
uv run --script run.py experiment1       # Single experiment (1-8)
uv run --script run.py all              # All 8 experiments
uv run --script run.py experiment3       # Noisy perception
```

Statistical analysis:
```
uv run --script analyze_stats.py all     # All experiments
uv run --script analyze_stats.py exp1    # Single experiment
uv run --script analyze_stats.py summary # Cross-experiment summary
```

Visualization:
```
uv run --script visualize.py             # Generate all plots
```

## Project structure

- `model.py` — Core pigeonhole system (numpy backend)
- `perturbations.py` — Hook-based perturbations (freeze, noise, misleading, etc.)
- `experiments.py` — 8 experiment functions
- `metrics.py` — Statistical metrics (DG index, robustness curves, etc.)
- `run.py` — CLI dispatcher
- `analyze_stats.py` — Paired t-tests and summary tables
- `visualize.py` — Matplotlib plotting functions
- `results/` — JSON result files + PNG plots
- `docs/PAPER.md` — Main paper

## Experiments

1. Frozen hole robustness curve
2. Policy comparison (GREEDY, EXPLORATORY, REPULSIVE, COOPERATIVE)
3. Noisy perception (Gaussian noise on reported loads)
4. View radius sweep (pigeon visibility range)
5. Chimeric policies (mixed-policy populations)
6. Recovery after damage (freeze then heal)
7. Progressive vs sudden damage (stress inoculation)
8. Misleading holes (deceptive substrate)
