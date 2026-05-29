# Claim Ledger

Every numeric claim in `PAPER.md` traced to the committed simulation output.
The experiments are seeded and deterministic; regenerate the entire trail with:

```
uv run --script run.py all          # writes results/experiment{1..8}*.json
uv run --script analyze_stats.py all # paired t-tests, Cohen's d, Spearman rho
uv run --script visualize.py         # results/exp*.png
```

Regenerated 2026-05-29; all values below reproduce the paper exactly (the
results had simply never been committed). Base model `m=10, n=7` (so
`O_min = m − n = 3`), `n=30` reps, 500 steps, paired t-tests with matched seeds.

| # | Claim | Source | Value | ✓ |
|---|---|---|---|---|
| 1 | `O_min = m − n = 3` is the irreducible minimum overload | model + `experiment1_frozen_robustness.json` (frozen_0) | 3.00 | [x] |
| 2 | In six of eight experiments every run converges to the configuration's `O_min` with zero-variance final overload; the exceptions are noise (exp 3) and misleading holes (exp 8) | `experiment{1,2,4,5,6,7}*.json` | 3.0 / 4.0 endpoints, zero variance | [x] |
| 3 | Noise: monotonic degradation, no tolerance threshold; ρ = +0.638, p < 0.0001 | `experiment3_noisy_perception.json` | +12.2% (p=0.0011, d=0.66) → +43.3% (d=1.85) | [x] |
| 4 | View radius changes convergence speed, not destination (all reach `O_min=3`) | `experiment4_view_radius.json` | conv −49% / −67% / −81% / −83% | [x] |
| 5 | All four policies reach identical overload (4.0 under 1 frozen hole); process cost varies >5×; same-target retry 0.463 (REPULSIVE) → 0.997 (COOPERATIVE) | `experiment2_policy_comparison.json` | failed placements 84.6 → 460.3 | [x] |
| 6 | Chimeric mixed-policy populations reach the same endpoint (4.0); aggregation index 0.738–0.796 | `experiment5_chimeric.json` | 4.0 all pairs | [x] |
| 7 | Recovery: damage and damage+heal both end at 3.0; healing halves wasted actions (49.4 → 24.7 failed placements) | `experiment6_recovery.json` | 3.0 endpoint | [x] |
| 8 | Progressive vs sudden damage: identical 3.0 endpoint; gradual yields 26% fewer failed placements (173.5 → 128.9); DG index 0 | `experiment7_progressive_damage.json` | 3.0 endpoint | [x] |
| 9 | Misleading holes invert the pattern: overload +25.6% → +46.7%; single misleading hole (14% of substrate) captures 36% of pigeons and 66% of overload; ρ = +0.417, p < 0.0001 | `experiment8_misleading_holes.json` | occupancy bias +0.217 → +0.080 | [x] |
| 10 | Delayed-gratification index = 0.0 in all conditions (no agent-level learning) | all experiments | DG = 0.0 | [x] |
