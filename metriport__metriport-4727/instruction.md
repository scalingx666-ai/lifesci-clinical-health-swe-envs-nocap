# Issue

**Title:** feat(ap): bump to two weeks

## Description

Ref: ENG-000

### Description

- bumping PD rerun to 2 weeks for initial rollout

### Testing

- Local
  - [ ] N/A
- Staging
   - [ ] N/A
- Sandbox
   - [ ] N/A
- Production
   - [ ] N/A

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Refactor**
  * Optimized document link enrichment with parallel processing for faster, more consistent results and clearer logging.

* **Chores**
  * Increased the stale data lookback from 1 to 2 weeks, reducing unnecessary background re-queries and improving overall efficiency.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `040bd5974e4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.