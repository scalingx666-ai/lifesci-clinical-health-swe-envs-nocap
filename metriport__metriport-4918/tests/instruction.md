# Issue

**Title:** ENG-1110 Normalize ejection fraction units

## Description

Part of ENG-1110

### Description

- Normalize ejection fraction units to %, mL, or mL/m2

### Testing

- Local
  - [x] Convert a file that had a bad unit
- Production
  - [ ] Reprocess an affected patient

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Enhanced unit normalization for Ejection Fraction measurements in medical observations, ensuring consistent standardization of measurement units across different formats (e.g., milliliters, percentages).

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1bfe4f2cb7f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.