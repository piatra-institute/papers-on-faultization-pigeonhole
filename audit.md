# Audit

Dated log of editorial passes and verification runs. Newest first.

## 2026-05-29 — upgrade pass (Group C): closed the results gap

The paper carried ~30 numeric claims with no committed result artifacts
(`claims_target: none`, empty `results/`). The voice was already clean (no
em-dashes, flat declaratives), so this pass is about reproducibility, not prose.

Changes:
- Regenerated the full result trail (seeded, deterministic): `run.py all` →
  8 `experiment*_*.json`; `analyze_stats.py all` → paired t-tests, Cohen's d,
  Spearman ρ; `visualize.py` → 8 PNGs. Total runtime ~10s.
- Verified every regenerated number against the prose and `FINDINGS.md`: all
  reproduce exactly (e.g. noise +12.2%/p=0.0011 → +43.3%; misleading +25.6% →
  +46.7%; occupancy bias +0.217; ρ=+0.638 and +0.417). No drift — the results
  had simply never been committed.
- Added `docs/CLAIM_LEDGER.md` (10 headline claims → source result file →
  verified value) and set `claims_target: claim-ledger`.
- Citation hygiene: replaced the placeholder `arXiv:2503.XXXXX` on Kofman, Bhatt
  & Levin (2025) with "Preprint." The Levin (2026) entry is honestly labelled
  ("Blog post, March 31, 2026") with a real locator and was left as is.

Verification: voice 0 errors; claims => claim-ledger present, all rows verified;
build clean; check => PASS. Results + figures now committed.
