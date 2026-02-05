# TTGOS Evidence

This repository is the public evidence & verification hub for TTGOS benchmark results.

## About TTGOS and MELQI

**TTGOS** is an open-source project maintained by **Hironao Nakamura** as an independent research effort, and it is the reference implementation used to support his research papers.
**MELQI** refers to the broader program that organizes the overall initiative around verification, reproducibility, and related infrastructure, also run by Hironao Nakamura.
**MELQI LTD** is his sole-director company whose role is conformance/verification operations (as described on its company page).
The evidence bundles linked from this repository are derived from TTGOS runs and should be attributed to the TTGOS research project, not to MELQI LTD.

- [Hironao Nakamura (profile)](https://www.melqi.org/people/hironao/)
- [TTGOS OSS repository](https://github.com/hironao-nakamura/two-topos-grounding-os)
- [MELQI LTD (company page)](https://www.melqi.org/ltd/)

## 30-second summary
We achieve **CuP-SOTA** on **ST-WebAgentBench Core-84** with **GPT-5.2 + TTGOS Guard**:

- **CuP (Guard)**: 46.4% (39/84)
- **CuP (Baseline, same model)**: 19.0% (16/84)
- **Guard effect (same model)**: +27.4 points
- **Violations**: 0 (Guard & Baseline)
- Evidence is auditable: receipts per success + validator PASS

## Benchmark (primary sources)

ST-WebAgentBench is a benchmark developed and introduced by researchers at IBM Research.

- Official site: [ST-WebAgentBench](https://sites.google.com/view/st-webagentbench)
- GitHub: [segev-shlomov/ST-WebAgentBench](https://github.com/segev-shlomov/ST-WebAgentBench)
- Paper (arXiv): [2410.06703](https://arxiv.org/abs/2410.06703)
- Paper (OpenReview): [forum page](https://openreview.net/forum?id=IIzehISTBe)
- IBM Research publication: [ST-WEBAGENTBENCH](https://research.ibm.com/publications/st-webagentbench-a-benchmark-for-evaluating-safety-and-trustworthiness-in-web-agents)
- Leaderboard (reference): core benchmark CuP for AWM is listed as 23.8%

## Evidence (download)
See:
- `benchmarks/stweb-core84/artifacts/manifest.json`
- `benchmarks/stweb-core84/artifacts/links.md`
- `benchmarks/stweb-core84/artifacts/sha256.txt`

These provide URLs + sha256 for:
- Core-84 Guard evidence bundle
- Core-84 Baseline evidence bundle
- Supplementary full-suite runs (included as supporting material; not part of the one-page claim)

## Reproduce (Hosted Repro)

TTGOS Hosted Repro lets third parties reproduce runs and obtain an auditable evidence bundle without proprietary source access.

- [Request API key](https://hironao-nakamura.github.io/ttgos-evidence/request-api-key.html)
- [API Guide](docs/api-guide.md)
- [API Access Policy](contracts/API_Access_Policy_v0.1.md)

## Public Verification Contract (v0.1)
Minimal public specs to verify evidence bundles:
- `contracts/Conformance_Spec_v0.1.md`
- `contracts/Validator_Rules_v0.1.md`
- `contracts/Receipt_Schema_v0.1.json`
- `contracts/Auditor_Report_Format_v0.1.md`
- `contracts/Verification_Template_v0.1.md`

## Benchmarks
- ST-WebAgentBench Core-84: `benchmarks/stweb-core84/`

## Contact
- General inquiries & feedback: hiro@melqi.org
- Issues: https://github.com/hironao-nakamura/ttgos-evidence/issues
