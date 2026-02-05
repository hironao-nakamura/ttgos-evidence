# SOTA Claim: ST-WebAgentBench Core-84 (CuP)

## Claim (Core-84)
We achieve **CuP-SOTA** on **ST-WebAgentBench Core-84 (task IDs 0..83)** with an auditable evidence bundle:

- **Model**: gpt-5.2-2025-12-11
- **CuP (Guard)**: **39/84 = 46.4%**
- **CuP (Baseline, same model)**: **16/84 = 19.0%**
- **Guard effect (same model ablation)**: **+27.4 points**
- **Violations**: 0 (Guard & Baseline)
- Evidence: receipts per CuP-success task + validator PASS

## Why this is not "just a stronger model"
We include an ablation under identical conditions:
- Same benchmark lock, task set, model, timeout, and step budget.
- Only the Guard layer differs.
- CuP increases from 19.0% to 46.4% (+27.4 points).

## Evidence bundles (auditable)
All downloadable artifacts and sha256 digests:
- `artifacts/manifest.json`
- `artifacts/links.md`
- `artifacts/sha256.txt`

The evidence bundles include:
- `version_lock.json` (benchmark commit + task sha256 + engine build id)
- `environment.json`
- `summary.json` (84 tasks)
- `receipts_v0_1/` (one receipt per CuP-success)
- `validator_report.json` (PASS/FAIL)

## Benchmark (primary sources)
- Official site: [ST-WebAgentBench](https://sites.google.com/view/st-webagentbench)
- GitHub: [segev-shlomov/ST-WebAgentBench](https://github.com/segev-shlomov/ST-WebAgentBench)
- Paper (arXiv): [2410.06703](https://arxiv.org/abs/2410.06703)
- Paper (OpenReview): [forum page](https://openreview.net/forum?id=IIzehISTBe)

## Notes
- The public one-page claim is **Core-84 only**.
- Supplementary full-suite runs are provided in the EvidencePack as supporting material.
