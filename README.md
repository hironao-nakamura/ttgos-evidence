# TTGOS Evidence

This repository is the public evidence & verification hub for TTGOS benchmark results.

## About TTGOS and MELQI

**TTGOS** is a safety framework for autonomous AI agents maintained by **Hironao Nakamura** as an independent research effort, and it is the reference implementation used to support his research papers.
**MELQI** refers to the broader program that organizes the overall initiative around verification, reproducibility, and related infrastructure, also run by Hironao Nakamura.
**MELQI LTD** is his sole-director company whose role is conformance/verification operations (as described on its company page).
The evidence bundles linked from this repository are derived from TTGOS runs and should be attributed to the TTGOS research project, not to MELQI LTD.

- [Hironao Nakamura (profile)](https://www.melqi.org/people/hironao/)
- [TTGOS repository](https://github.com/hironao-nakamura/two-topos-grounding-os)
- [MELQI LTD (company page)](https://www.melqi.org/ltd/)

## 30-second summary

**OS-Harm** (NeurIPS 2025 Spotlight): **100% Execution Safety** — 110/110 harmful tasks prevented, 3 runs, 2 models, 0 harm executed. Best paper baseline ~59%.

**ST-WebAgentBench** (IBM Research): **CuP-SOTA** — 46.4% (39/84) vs 19.0% baseline (+27.4pt), 0 violations, validator PASS.

One framework, model-agnostic, multiple benchmarks. All evidence is auditable and downloadable.

## Benchmarks (primary sources)

### OS-Harm (EPFL & CMU)
- GitHub: [tml-epfl/os-harm](https://github.com/tml-epfl/os-harm)
- Paper (arXiv): [2506.14866](https://arxiv.org/abs/2506.14866)
- OpenReview: [forum page](https://openreview.net/forum?id=kNHA0QCSQa)
- NeurIPS 2025: [poster](https://neurips.cc/virtual/2025/poster/121772)

### ST-WebAgentBench (IBM Research)
- Official site: [ST-WebAgentBench](https://sites.google.com/view/st-webagentbench)
- GitHub: [segev-shlomov/ST-WebAgentBench](https://github.com/segev-shlomov/ST-WebAgentBench)
- Paper (arXiv): [2410.06703](https://arxiv.org/abs/2410.06703)
- Paper (OpenReview): [forum page](https://openreview.net/forum?id=IIzehISTBe)
- IBM Research publication: [ST-WEBAGENTBENCH](https://research.ibm.com/publications/st-webagentbench-a-benchmark-for-evaluating-safety-and-trustworthiness-in-web-agents)

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

## Results pages
- **OS-Harm**: [osharm.html](https://hironao-nakamura.github.io/ttgos-evidence/osharm.html) — 100% execution safety, ablation study, evidence downloads
- **ST-WebAgentBench**: [stweb.html](https://hironao-nakamura.github.io/ttgos-evidence/stweb.html) — CuP-SOTA, evidence downloads, hosted repro

## Contact
- General inquiries & feedback: hiro@melqi.org
- Issues: https://github.com/hironao-nakamura/ttgos-evidence/issues
