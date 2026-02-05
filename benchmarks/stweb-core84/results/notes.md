# Results Notes

## Core-84 Task Set

- Official benchmark subset from ST-WebAgentBench
- 84 tasks selected for evaluation

## Results Summary

| Variant | CuP | Tasks | Violations | Timeouts |
|---------|-----|-------|------------|----------|
| Guard | 46.4% | 39/84 | 0 | 7 |
| Baseline | 19.0% | 16/84 | 0 | 7 |
| **Guard effect** | **+27.4 pt** | — | — | — |

## Important Notes

1. **CuP metric**: Completion under Policy = completed AND compliant
2. **Violations = 0**: Both guard and baseline achieved zero policy violations
3. **Receipts**: Generated in the same run (no post-hoc replays)
4. **Full235**: Supplementary runs included in EvidencePack but NOT part of public claim

## Leaderboard Reference

- AWM CuP 23.8% (Core benchmark)
- This is the published leaderboard reference value

## Run IDs

- Guard: `20260204T010704Z_97799f`
- Baseline: `20260204T034744Z_d661df`
