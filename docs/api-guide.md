# TTGOS Hosted Repro - API Guide

This guide explains how to run ST-WebAgentBench evaluations using the TTGOS Hosted Repro API.

## Prerequisites

- **TTGOS API Key**: [Register here](request-api-key.html) (format: `ttgos_xxx...`)
- **OpenAI API Key**: Your own OpenAI API key with access to the model you want to evaluate

## API Endpoint

```
https://jxvg5033zf.execute-api.us-east-2.amazonaws.com
```

## Step 1: Submit an Evaluation Job

```bash
curl -X POST https://jxvg5033zf.execute-api.us-east-2.amazonaws.com/v1/jobs \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <YOUR_TTGOS_API_KEY>" \
  -H "X-OpenAI-Api-Key: <YOUR_OPENAI_API_KEY>" \
  -d '{
    "mode": "guard",
    "model": "gpt-5.2-2025-12-11",
    "tasks": "0-83"
  }'
```

### Request Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `mode` | No | `guard` | Evaluation mode: `guard`, `baseline`, or `both` |
| `model` | No | `gpt-5.2-2025-12-11` | OpenAI model ID to evaluate |
| `tasks` | No | `0-83` | Task range (e.g., `0-83` for all 84 tasks, `0-9` for first 10) |

### Response

```json
{
  "api_version": "1.0",
  "job_id": "job_20260205T034615Z_30c058",
  "status": "queued",
  "engine_build_id": "...",
  "benchmark_commit": "...",
  "task_file_sha256": "..."
}
```

Save the `job_id` for the next steps.

## Step 2: Check Job Progress

```bash
curl https://jxvg5033zf.execute-api.us-east-2.amazonaws.com/v1/jobs/<JOB_ID> \
  -H "Authorization: Bearer <YOUR_TTGOS_API_KEY>"
```

### Response

```json
{
  "api_version": "1.0",
  "job_id": "job_20260205T034615Z_30c058",
  "status": "running",
  "tasks_done": 42,
  "tasks_total": 84,
  "created_at": "2026-02-05T03:46:15.704628+00:00",
  "started_at": "2026-02-05T03:46:15.921117+00:00",
  "finished_at": null,
  "error_message": null
}
```

### Job Status Values

| Status | Description |
|--------|-------------|
| `queued` | Job is waiting to be picked up by a worker |
| `running` | Job is currently executing |
| `done` | Job completed successfully |
| `failed` | Job failed (check `error_message`) |

## Step 3: Download Evidence Bundle

Once the job status is `done`, download the evidence bundle:

```bash
curl https://jxvg5033zf.execute-api.us-east-2.amazonaws.com/v1/jobs/<JOB_ID>/bundle \
  -H "Authorization: Bearer <YOUR_TTGOS_API_KEY>"
```

### Response

```json
{
  "api_version": "1.0",
  "job_id": "job_20260205T034615Z_30c058",
  "bundle_url": "https://...",
  "bundle_sha256": "4aab06be2449028de86166cc53bff68988d423c2bf2899f1e4b26651bc80d267"
}
```

Download the bundle using the presigned URL:

```bash
curl -o evidence_bundle.tar.gz "<BUNDLE_URL>"
```

Verify the SHA256 hash:

```bash
shasum -a 256 evidence_bundle.tar.gz
# Should match: 4aab06be2449028de86166cc53bff68988d423c2bf2899f1e4b26651bc80d267
```

## Step 4: Inspect the Evidence Bundle

Extract the bundle:

```bash
tar -xzf evidence_bundle.tar.gz
```

### Bundle Contents

```
evidence_bundle/
├── signature.txt              # HMAC signature for integrity verification
├── sha256.txt                 # SHA256 hash of bundle contents
├── AUTO_VERIFICATION_REPORT.md  # Human-readable summary
├── A_bench_definition/
│   └── version_lock.json      # Benchmark version info
├── B_environment/
│   └── environment.json       # Execution environment settings
├── C_execution_evidence/
│   └── summary.json           # Task-by-task results
├── D_reports/
│   └── validator_report.json  # Validation results
└── E_repro/
    ├── run_command.txt        # Command used to run evaluation
    └── git_info.json          # Git commit info
```

### Key Results in `summary.json`

```json
{
  "model": "gpt-5.2-2025-12-11",
  "variant": "guard",
  "tasks": {
    "guard": {
      "0": {
        "task_id": 0,
        "finished": true,
        "cup": true,
        "violations_count": 0,
        "error_message": null
      },
      ...
    }
  }
}
```

| Field | Description |
|-------|-------------|
| `finished` | Whether the task completed without errors |
| `cup` | Correct Under Policy - task succeeded according to policy |
| `violations_count` | Number of policy violations detected |

## Complete Example Script

```bash
#!/bin/bash

TTGOS_API_KEY="ttgos_xxx..."
OPENAI_API_KEY="sk-proj-xxx..."
API_BASE="https://jxvg5033zf.execute-api.us-east-2.amazonaws.com"

# 1. Submit job
echo "Submitting job..."
RESPONSE=$(curl -s -X POST "$API_BASE/v1/jobs" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TTGOS_API_KEY" \
  -H "X-OpenAI-Api-Key: $OPENAI_API_KEY" \
  -d '{
    "mode": "guard",
    "model": "gpt-5.2-2025-12-11",
    "tasks": "0-83"
  }')

JOB_ID=$(echo "$RESPONSE" | jq -r '.job_id')
echo "Job ID: $JOB_ID"

# 2. Poll for completion
echo "Waiting for completion..."
while true; do
  STATUS_RESPONSE=$(curl -s "$API_BASE/v1/jobs/$JOB_ID" \
    -H "Authorization: Bearer $TTGOS_API_KEY")

  STATUS=$(echo "$STATUS_RESPONSE" | jq -r '.status')
  DONE=$(echo "$STATUS_RESPONSE" | jq -r '.tasks_done')
  TOTAL=$(echo "$STATUS_RESPONSE" | jq -r '.tasks_total')

  echo "Status: $STATUS ($DONE/$TOTAL tasks)"

  if [ "$STATUS" = "done" ] || [ "$STATUS" = "failed" ]; then
    break
  fi

  sleep 30
done

# 3. Download bundle
if [ "$STATUS" = "done" ]; then
  echo "Downloading bundle..."
  BUNDLE_RESPONSE=$(curl -s "$API_BASE/v1/jobs/$JOB_ID/bundle" \
    -H "Authorization: Bearer $TTGOS_API_KEY")

  BUNDLE_URL=$(echo "$BUNDLE_RESPONSE" | jq -r '.bundle_url')
  EXPECTED_SHA=$(echo "$BUNDLE_RESPONSE" | jq -r '.bundle_sha256')

  curl -s -o "evidence_bundle_$JOB_ID.tar.gz" "$BUNDLE_URL"

  # Verify hash
  ACTUAL_SHA=$(shasum -a 256 "evidence_bundle_$JOB_ID.tar.gz" | cut -d' ' -f1)
  if [ "$ACTUAL_SHA" = "$EXPECTED_SHA" ]; then
    echo "Bundle verified successfully!"
  else
    echo "WARNING: SHA256 mismatch!"
  fi
fi
```

## Troubleshooting

### Error: "Invalid or missing API key"
- Ensure the `Authorization` header uses the `Bearer` prefix
- Check that your TTGOS API key is correct

### Error: "X-OpenAI-Api-Key header is required"
- Add the `X-OpenAI-Api-Key` header with your OpenAI API key

### Job status is "failed"
- Check the `error_message` field in the job status response
- Common issues: invalid model name, OpenAI API key issues

## Support

For issues or questions, please open an issue at the [ttgos-evidence repository](https://github.com/hironao-nakamura/ttgos-evidence/issues).
