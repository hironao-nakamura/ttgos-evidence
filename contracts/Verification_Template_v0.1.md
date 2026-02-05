# MELQI Hosted Repro — Verification Template v0.1
(Observation-only; endorsement not required)

## 1. Verifier Identity (optional)
- Name / org (or "Anonymous"):
- Contact (optional):
- Conflict of interest (optional):

## 2. What I Ran (required)
- Date (UTC):
- Hosted Repro API version:
- Job ID:
- Evidence bundle ID:
- benchmark_commit:
- task_file_sha256:
- engine_build_id:
- Task set: Core-84 / Subset IDs:
- Model:
- timeout_seconds_per_task:
- max_steps_per_task:
- seed_policy:

## 3. What I Observed (required)
- CuP: __ / __ (= __%)
- CR (if available): __ / __ (= __%)
- Total violations: __
- Risk Ratio: __
- Timeouts (both / guard-only / baseline-only): __ / __ / __

### Spot-check A (success)
- task_id:
- receipt file:
- final_url (or pattern):
- URL check passed: yes/no
- DOM checks summary:
- screenshot present: yes/no

### Spot-check B (failure)
- task_id:
- error_type / error_message:
- notable behavior:

## 4. Publication Preference (required)
- Publish as-is / publish with redactions / do not publish
- Attribution: name/org / pseudonym / anonymous
