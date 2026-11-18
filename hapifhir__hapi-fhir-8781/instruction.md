# Issue

**Title:** updating query that generates metrics to take into account partitions

## Description

**Issue**

`MdmMetricSvcJpaImpl.generateMdmMetrics` applied the request's `RequestPartitionId` to its resource counts only. The link-type counts (`generateLinkMetrics`) and the match-score distribution (`generateLinkScoreMetrics`) were computed across all partitions, ignoring the partition passed in.
On a partitioned server, a metrics request scoped to one partition returned link/score counts aggregated over every partition — inconsistent with the resource counts in the same response, and a cross-partition information exposure.

**Changes**

- `IMdmLinkJpaMetricsRepository` — added new query `generateMetricsForPartitions`, the existing link-metrics query plus `AND ml.myPartitionIdValue IN (:partitionIds)`. The original generateMetrics is retained for the unscoped path.
- `MdmMetricSvcJpaImpl` — `generateLinkMetrics` and `generateLinkScoreMetrics` now apply the partition filter when a specific partition is requested. A new `getPartitionIdsToFilterOrNull` helper returns the partition ids to filter on, or null for no-partition / all-partitions requests — in which case the existing aggregate-across-all behavior is preserved (no regression for non-partitioned servers or existing callers).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1882d964ede8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.