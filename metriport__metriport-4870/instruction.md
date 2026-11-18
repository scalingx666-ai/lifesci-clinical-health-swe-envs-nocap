# Issue

**Title:** ENG-1285: set up new per-cx ai summaries

## Description

### Dependencies

None

### Description

New AI summaries for custom CXs as described in these tickets:
- https://linear.app/metriport/issue/ENG-1285/enable-custom-ai-summary
- https://linear.app/metriport/issue/CS-2598/implement-ai-summary
- ?? There's a third one, having trouble finding it.

### Testing

- Local
  - [x] Run AI summary gen for each of 3 new cases.

### Release Notes

- [ ] Set cx FFs for different custom summaries
- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added AI brief modes for Cardiac Care and Nitrates & Conditions, providing structured patient summaries when enabled.
  * Enhanced Recent Visit summaries with clearer sections; refined summaries now merge prior outputs while retaining structure.

* **Chores**
  * Introduced rollout controls to enable new AI brief modes per customer.
  * Initialized feature flags in the local medical-records script for consistent behavior.

* **Documentation**
  * Updated local script guidance to reflect feature-flag initialization and AI summary behavior.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ae359097422b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.