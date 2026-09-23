# On Faultization: Pigeonhole

Coverage and Failure in a Pigeonhole Model.

Load-seeking allocation rules can be drawn toward a resource that refuses entry, because a closed resource reports the lowest load. We study this failure in a small allocation model in which ten items move among seven holes using sampled load reports. The pigeonhole bound constrains fully placed assignments, but the usual overload measure records coverage and says nothing about balance, and it improves when items become unplaced. A paired audit separates placement, coverage and balance, gives every condition the same random inputs, and compares load-seeking rules with random movement, staying put, and an arrival-aware comparison. Across thirty seed tapes, closing five holes leaves a mean of 5.03 items unplaced under the original comparison rule. Sampling every hole does not help, whereas trying another candidate after rejection places every item. The effect of tiny Gaussian errors depends on how noisy loads are encoded: truncation and unquantized reports both worsen allocation, while nearest-integer rounding preserves the noiseless result at the smallest tested scale. Accounting for the arriving item prevents that endpoint loss, although movement continues. Blocking entry to a hole preserves its existing occupancy, whereas eviction creates a separate recovery problem. The failures lie in admission information and in local cost comparisons. The results support a method for inspecting perturbation models and license no further inference about cognition or access to mathematical patterns.

## Read and reproduce

The current manuscript is [paper/PAPER.md](paper/PAPER.md). Build its local PDF with `python3 build.py` from this directory; Pandoc and XeLaTeX are required. The builder splits the title at its first colon, then prints the institutional author and date on separate lines. The generated PDF, build log and manifest remain local and ignored by Git.

The [audit protocol](simulation/AUDIT_PROTOCOL.md) specifies the exploratory redesign before its new outcomes. From `simulation/`:

```sh
python3 -m unittest test_audit -v
uv run --script audit.py --output output/my-audit
```

The second command uses pinned script dependencies and a fresh output path. With the recorded dependencies already installed, `python3 audit.py` also works. Do not rerun against the canonical output directory: the runner refuses an existing result file. No external data are needed.

## Evidence

The canonical scientific results and figures are in [simulation/output/september-audit/](simulation/output/september-audit/). [verification/september-audit.json](verification/september-audit.json) records execution and hashes. [claims.yaml](claims.yaml) binds selected manuscript claims to results and sources; [source-checks.md](source-checks.md) records what was actually checked. Editorial and visual reviews identify the exact artifacts reviewed. Local verification does not certify deployment or external validity.

The eight old experiment JSON files and original model remain unchanged. `CLAIM_LEDGER.md`, the old findings/experiment reports and the June referee report are historical, not verification for this revision. Their claims about convergence, noise tolerance, equal information access and pattern access should not be carried forward.
