# Issue

**Title:** ENG-1304: fix format date

## Description

### Dependencies

None

### Description

serviceStartTime + serviceEndTime were having their hour/minute/second granularity set to all 0s by the formatDate utility. This PR creates a similar formatDatetime utility that does not drop the hms granularity as this is relevant + real information about when the medical service provided took place, with h/m/s granularity.

### Testing

- Local
  - [x] Check that more granular period is created in the resulting docref for a patient
- Staging
  - [ ] Check that more granular period is created in the resulting docref for a patient
- Production
  - [ ] Check that more granular period is created in the resulting docref for a patient

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Service period information now includes time components, providing enhanced scheduling precision beyond date-only data.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b479f900318`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.