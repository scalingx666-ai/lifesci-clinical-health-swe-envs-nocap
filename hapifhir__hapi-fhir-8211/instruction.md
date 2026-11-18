# Issue

**Title:** Enforce merge resource-limit across all partitions

## Description

## Problem

Patient `$merge` accepts a `resource-limit` parameter capping how many resources a single merge may
touch; a merge that would exceed it is rejected with a 412 instead of being performed. Two separate gaps
let merges past that limit.

**1. On multi-database deployments, only one database was counted.** The count ran inside a transaction
bound to a single partition. Where a partition is a separate database, that transaction reaches only one
of them, so referring resources held on other shards were never counted.

Single-database deployments were unaffected by this one: the `ResourceLink` query carries no partition
predicate, so within one database it already returned every partition's rows, whatever the transaction
was scoped to.

**2. Resources pulled in indirectly were never counted anywhere.** When a merge moves a compartment
resource to another partition, that resource takes a new id, so everything referencing it must be
rewritten too — even though none of those resources ever referenced the merge source. The limit counted
only direct referrers, so these were invisible to it. This one is not specific to multiple databases; it
affects any *partition-aware* merge — one that has to relocate resources from one partition to another
instead of patching them where they sit, which is what gives them new ids in the first place.

## Changes

### Fix

The exact count is not available while checking is still cheap, and is no longer cheap by the time it is
exact. So the limit is enforced twice:

1. **Up-front count** — one query, now across all partitions. Counts only *direct* referrers, so it is a
   lower bound. Rejects an obviously oversized merge before all resources are loaded, and is the
   number reported by `preview` — a `$merge` run with `preview=true`, which reports what the merge would
   change without changing anything.
2. **Plan count** in `PartitionAwareReplaceReferencesSvc` — authoritative, taken once the full change set
   is known, immediately before the single `transactionNested` write. It also catches resources that
   reference resources *moved* by the merge and so never referenced the source. Rejecting here commits
   nothing.

Every direct referrer ends up in the plan, so the up-front count is always ≤ the plan count — the two
cannot contradict each other.

`preview` now reports a lower bound ("would update at least N") when the merge is partition-aware. For a
same-partition merge the count is exact and the message is unchanged.

The all-partition methods use `searchList`, not `execute` — only the former fans out where partitions are
separate databases. That is the trap the original code fell into.

### Refactoring

- `ReferencingResourcesQuerySvc` collects the referrer queries in one place and names their partition
  scope in the method, so a mismatch like this is visible at the call site.
- Removes `IReplaceReferencesSvc.countResourcesReferencingResource`, which had no callers anywhere.

## No changelog entry

The affected support — cross-partition Patient `$merge` / `$undo-merge` for multi-database Patient ID
mode partitioning (#8185) — landed on 2026-07-27 and is not contained in any release tag. It ships for
the first time in this same release, so there is no released version in which a user could have hit this
bug.

## Tests

`PatientIdModePatientMergeR4Test$ResourceLimitAcrossPartitions`, one test per check:

- Direct referrers count toward `resource-limit` even when they sit in different partitions.
- The limit also counts *indirect* referrers — resources that never referenced the source at all, but
  which the merge must still rewrite because a resource they do reference changes partition and takes a
  new id. Verified to fail without the fix: the merge silently completed over its limit.

Each asserts its own message code, so it is clear which check rejected.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c02b79630ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.