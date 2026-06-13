# Audit

Dated log of editorial passes and verification runs. Newest first.

## 2026-06-13 — voice reform

Voice-reform pass to remove AI-writing tells, per `tooling/docs/voice.md`. No numbers, equations, table values, or citations changed.

- Reduced voice review-candidates 19 → 6 (0 errors throughout). Thinned the dominant "pattern-channeling, not learning" / "the pattern, not the policy" inline-contrastive tic across the abstract, Results (Exp 1, 6, 7), and Discussion (5.4, 5.6) by rewriting as positive declaratives ("the pattern channels the convergence; agent-level learning does not", "the pattern determines the outcome; the policy merely accesses it", "the interface itself, rather than the pattern, sets the fidelity requirement"). Rewrote "discovered, not created" framing in the introduction with "rather than".
- Density: deleted reflexive "exactly"/"precisely" scope-hedges in the introduction (signature exactly 6 → 3, precisely 3 → 2); left literal/mathematical "exactly one hole" and "exactly $O_{\min}$" uses intact.
- Structure unchanged (6 numbered sections, no structure advisory). Tricolon proxy 58 (advisory; residual is in the cross-experiment summary phrasing).

Verify: `voice` 0 errors; `refs` 0 missing, 9 in-text keys / 11 entries, 2 pre-existing unused (Simon 1956 and one other, not introduced here); `build` clean (0 missing-char); `check` => PASS.

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
