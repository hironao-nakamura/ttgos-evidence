# TTGOS Evidence

Public evidence & verification hub for [TTGOS](https://github.com/hironao-nakamura/two-topos-grounding-os) benchmark results.

## Key results

**OS-Harm** (NeurIPS 2025 Spotlight): **100% Execution Safety** — 110/110 harmful tasks prevented, 3 runs, 2 models, 0 harm executed. Best paper baseline ~59%.

**ST-WebAgentBench** (IBM Research): **CuP-SOTA** — 46.4% (39/84) vs 19.0% baseline (+27.4pt), 0 violations, validator PASS.

One framework, model-agnostic, multiple benchmarks. All evidence is auditable and downloadable.

## Results pages

- **OS-Harm**: [osharm.html](https://hironao-nakamura.github.io/ttgos-evidence/osharm.html) — 100% execution safety, ablation study, evidence downloads
- **ST-WebAgentBench**: [stweb.html](https://hironao-nakamura.github.io/ttgos-evidence/stweb.html) — CuP-SOTA, evidence downloads, hosted repro

## Evidence (download)

### OS-Harm

All artifacts are on S3 (`s3://ttgos-evidence/artifacts/osharm/v1/`):

| File | Size | Description |
|------|------|-------------|
| `osharm_ttgos_evidence_v1.tar.gz` | 7 KB | Evidence pack (metrics, SOTA claim, reproduction info) |
| `run1_gpt52_guard_COMPLETE.tar.gz` | 388 MB | Run 1: GPT-5.2 + Guard (recordings, trajectories, judgments) |
| `run2_gpt41_guard_COMPLETE.tar.gz` | 564 MB | Run 2: GPT-4.1 + Guard |
| `run3_gpt52_noguard_COMPLETE.tar.gz` | 1.1 GB | Run 3: GPT-5.2 without Guard (ablation) |

Download links and SHA256 checksums are on the [OS-Harm results page](https://hironao-nakamura.github.io/ttgos-evidence/osharm.html#evidence).

### ST-WebAgentBench

See:
- `benchmarks/stweb-core84/artifacts/manifest.json`
- `benchmarks/stweb-core84/artifacts/links.md`
- `benchmarks/stweb-core84/artifacts/sha256.txt`

Download links are on the [ST-WebAgentBench results page](https://hironao-nakamura.github.io/ttgos-evidence/stweb.html#evidence).

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
- OpenReview: [forum page](https://openreview.net/forum?id=IIzehISTBe)
- IBM Research: [publication page](https://research.ibm.com/publications/st-webagentbench-a-benchmark-for-evaluating-safety-and-trustworthiness-in-web-agents)

## Reproduce (Hosted Repro)

TTGOS Hosted Repro lets third parties reproduce ST-WebAgentBench runs and obtain an auditable evidence bundle without proprietary source access.

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

## About

[TTGOS (Two-Topos Grounding OS)](https://github.com/hironao-nakamura/two-topos-grounding-os) is a safety framework for autonomous AI agents by [Hironao Nakamura](https://www.melqi.org/people/hironao/) (independent researcher). It provides model-agnostic safety guarantees, demonstrated across multiple benchmarks.

## Contact

- General inquiries & feedback: hiro@melqi.org
- Issues: https://github.com/hironao-nakamura/ttgos-evidence/issues
