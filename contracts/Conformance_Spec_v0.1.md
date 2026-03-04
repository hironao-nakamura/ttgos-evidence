# MELQI Verified Conformance Specification v0.1

## 0. Purpose
This document defines the minimal conformance contract for **MELQI Verified**.
It specifies what it means for a system to be *conformant* and what evidence must be produced
to support auditable verification.

This specification is intentionally minimal ("thin waist"):
- The **pass/fail conditions are public**.
- The **implementation strategy is not prescribed**.

## 1. Scope
This spec covers:
- Conformance claims for **ST-WebAgentBench Core-84** evaluation runs.
- Required evidence artifacts ("receipts") and their minimum fields.
- The definition of the reported metrics and their acceptance rules.

This spec does NOT cover:
- Internal algorithms (planning, recovery, heuristics).
- Model choice, prompting details, or proprietary execution logic.

## 2. Conformance Claim
A conformance claim MUST include:
- Benchmark identifier (e.g., `st-webagentbench`)
- Benchmark version lock:
  - `benchmark_commit`
  - `task_file_sha256`
- Task set identifier:
  - `core84` and task IDs `0..83`
- Engine identifier:
  - `engine_build_id` (immutable during the freeze window)
- Run configuration:
  - `model`
  - `timeout_seconds_per_task`
  - `max_steps_per_task`
  - `seed_policy` (fixed or explicitly declared as non-deterministic)
- Reported results:
  - `CuP` and numerator/denominator (e.g., `21/84`)
  - `violations_count`
  - `risk_ratio` (and per-dimension breakdown if available)

## 3. Required Artifacts
A conformant submission MUST provide:
1) **Run Summary**
   - A machine-readable `summary.json` containing per-task outcomes for the full task set.
2) **Receipts for Successful Tasks**
   - For each task counted as success under policy (CuP=True),
     provide a receipt file that includes at least:
     - final URL (or URL pattern match proof)
     - DOM checks used to verify end-state
     - timestamp
     - task_id
3) **Version Lock**
   - A `version_lock.json` containing benchmark and engine identifiers.
4) **Environment Description**
   - An `environment.json` containing the run configuration and major dependency versions.

Optionally, a submission MAY provide:
- Screenshots for successful tasks.
- Failure taxonomy logs and recovery traces.

## 4. Definitions
### 4.1 Completion Rate (CR)
CR is the fraction of tasks for which the task end-state is reached (regardless of policy).

### 4.2 Completion under Policy (CuP)
CuP is the fraction of tasks that are both:
- completed (end-state reached), and
- policy-compliant (violations_count == 0 for the task)

### 4.3 Violations
A violation is any recorded breach of an active policy during the task execution.

### 4.4 Risk Ratio
Risk Ratio quantifies policy breaches (typically normalized per policy dimension).
(Exact computation is defined by the benchmark evaluator; report raw values and, if available, per-dimension breakdown.)

## 5. Acceptance Criteria for a Conformance Report
A conformance report is accepted as "MELQI Verified Conformance Evidence v0.1" if:
- All required artifacts exist and are internally consistent.
- `summary.json` covers all tasks in the declared task set.
- Each CuP-success task has an associated receipt with required fields.
- `version_lock.json` and `environment.json` match the configuration declared in the claim.
- The engine build ID is within the declared freeze window (see API Access Policy).

Acceptance does NOT imply endorsement of safety beyond the reported benchmark scope.
It implies that the evidence package is auditable and conforms to this public contract.

## 6. Change Policy
- v0.1 is experimental and may change.
- Backward-compatible additions (new optional fields) are preferred.
- Breaking changes require a new major version and an explicit migration note.
