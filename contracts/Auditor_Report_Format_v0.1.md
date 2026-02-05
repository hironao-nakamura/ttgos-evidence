# MELQI Verified Auditor Report Format v0.1

## 0. Purpose
This document defines a minimal auditor report format for MELQI Verified conformance evidence.

## 1. Report Header (required)
- Report ID:
- Date (UTC):
- Prepared by: Name / org (or "Anonymous verifier")
- Scope:
  - Benchmark: ST-WebAgentBench
  - Task set: Core-84 (task IDs 0..83)
  - Engine build: <engine_build_id>
  - Benchmark commit: <benchmark_commit>
  - Task file SHA256: <task_file_sha256>

## 2. Run Configuration (required)
- Model:
- Timeout per task:
- Max steps per task:
- Seed policy:
- Headless:

## 3. Results Summary (required)
- CuP: <numerator>/<denominator> (= <percent>%)
- CR (if available): <numerator>/<denominator> (= <percent>%)
- Violations (total): <count>
- Risk Ratio: <value>

## 4. Evidence Package Integrity (required)
- Required files present: version_lock.json, environment.json, summary.json, receipts/
- Validator status: PASS/FAIL (if FAIL, list reason codes)

## 5. Receipt Spot-Checks (required)
Select at least:
- 2 CuP-success tasks (randomly chosen)
- 1 failure task (representative)

For each selected task:
- task_id
- receipt_id
- final_url
- URL check passed/failed
- DOM checks passed/failed (list selectors checked)
- (optional) screenshot reference

## 6. Notes on Method Limitations (required)
- timeouts and their interpretation
- non-determinism considerations
- scope limits (Core-84, commit lock, etc.)
- proprietary implementation not disclosed (if applicable)

## 7. Auditor Conclusion (required)
- Evidence Accepted / Accepted with Reservations / Rejected (with reasons)
