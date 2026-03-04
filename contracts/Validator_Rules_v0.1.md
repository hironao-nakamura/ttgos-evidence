# MELQI Verified Validator Rules v0.1
(Validator I/O and pass/fail rules)

## 0. Purpose
This document defines the public validator rules for verifying a conformance evidence package
without requiring access to proprietary implementation code.

## 1. Inputs
A validator consumes an **Evidence Bundle** directory or zip containing:

Required:
- `version_lock.json`
- `environment.json`
- `summary.json`
- `receipts/` directory (for CuP-success tasks)
- (optional) `screenshots/`

## 2. Outputs
The validator MUST produce:
- `validator_report.json` with:
  - `status`: PASS/FAIL
  - `fail_reasons`: array of machine-readable codes
  - `checked_task_set`: e.g., `core84`
  - `task_coverage`: counts
  - `receipt_coverage`: counts
  - `consistency_checks`: pass/fail items

## 3. Core Checks (PASS/FAIL)
### 3.1 Version Lock Integrity
FAIL if:
- `benchmark_commit` is missing
- `task_file_sha256` is missing
- `engine_build_id` is missing

### 3.2 Task Set Coverage
Given declared task set `core84`:
FAIL if:
- `summary.json` does not contain exactly 84 task entries for task IDs 0..83
- any task entry is missing required fields:
  - `task_id`
  - `finished` (bool)
  - `cup` (bool)
  - `violations_count` (int)
  - `error_type` or `error_message` (nullable)

### 3.3 CuP Accounting Consistency
FAIL if:
- The reported aggregate CuP numerator/denominator (if provided) does not match counting
  over `summary.json`.
Counting rule:
- A task counts toward CuP numerator iff `cup == true`.

### 3.4 Receipt Coverage for CuP-Success Tasks
For each task where `cup == true`:
FAIL if:
- corresponding receipt file is missing, OR
- receipt is missing required fields:
  - `task_id`
  - `timestamp`
  - `final_url` OR `url_pattern` + `url_match=true`
  - `dom_checks` (non-empty list)
Each `dom_checks` entry MUST include:
- `selector` (string)
- `check_type` (e.g., exists / exact_match / must_include)
- `observed` (string or boolean)
- `expected` (string or boolean)
- `passed` (bool)

### 3.5 Configuration Consistency
FAIL if:
- `environment.json.model` does not match `summary.json` header model (if present)
- `timeout_seconds_per_task` differs between environment and summary header (if present)
- `max_steps_per_task` differs between environment and summary header (if present)

### 3.6 Freeze Window Consistency (reference)
The validator SHOULD check:
- `engine_build_id` matches the build ID declared for the campaign window.
If the campaign window metadata is unavailable to the validator, it MUST record:
- `freeze_window_check: SKIPPED`

## 4. Recommended (Non-fatal) Checks
These do not fail validation but are reported:
- Presence of screenshots for CuP-success tasks.
- Presence of failure taxonomy logs.
- Presence of per-dimension risk breakdown.
- Presence of seed determinism declaration.

## 5. Minimal File Naming Convention
- receipts stored as: `receipts/task_<task_id>.json`
- screenshots stored as: `screenshots/task_<task_id>.png` (optional)

## 6. Rationale (non-normative)
These rules ensure:
- the benchmark definition is fixed (prevents "different benchmark" disputes),
- the full task set is accounted for,
- every claimed success has auditable end-state evidence,
- configuration is consistent across artifacts,
without disclosing proprietary implementation details.
