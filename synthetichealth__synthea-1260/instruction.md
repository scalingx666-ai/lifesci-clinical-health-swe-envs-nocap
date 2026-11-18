# Issue

**Title:** Repair inpatient encounter reason codes.

## Description

Repairing these inpatient encounter reasons also corrects weird primary diagnosis codes and admission codes in RIF exports.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `40cb89b520c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.