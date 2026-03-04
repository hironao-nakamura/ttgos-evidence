# MELQI Hosted Repro API Access Policy v0.1

## 0. Purpose
Defines access to MELQI Hosted Repro for reproducible benchmark runs without disclosing proprietary source.

## 1. Access Tiers
- Tier 0: Public docs (spec/rules/schemas)
- Tier 1: Verifier (API key; observation-only report requested)
- Tier 2: Auditor (NDA; limited deeper access)

## 2. Eligibility and Prioritization
Priority to applicants who intend to run reproducible jobs and submit observation-only reports.
Access is not contingent on positive feedback.

## 3. Freeze Window (Integrity Guarantee)
During an active verification campaign:
- engine build is fixed to one `engine_build_id`
- benchmark definition is fixed (`benchmark_commit`, `task_file_sha256`)
- no behavioral changes allowed
Post-freeze:
- frozen build remains runnable for at least 30 days

## 4. Evidence Bundle (What the API returns)
For each job:
- version_lock.json (benchmark_commit, task_file_sha256, engine_build_id, policy_hash if any)
- environment.json (model/timeout/steps/seed + major runtime versions)
- summary.json (per-task outcomes)
- receipts/ (for CuP-success tasks)
- human summary report

API response must include:
- api_version, job_id, engine_build_id, benchmark_commit, task_file_sha256, receipt_bundle_id

## 5. Verifier Reporting (Observation-only)
Verifiers are requested to submit Verification Template v0.1 (endorsement not required).
Critical reports are welcome.

## 6. Abuse Prevention
Rate limits, allowed task sets, and concurrent job limits may apply.
Access may be revoked if abused.

## 7. Disclaimers
Conformance evidence is benchmark-scoped and not a general safety certification.

## 8. Contact
- General inquiries & feedback: hiro@melqi.org
- Issue reporting: https://github.com/hironao-nakamura/ttgos-evidence/issues
