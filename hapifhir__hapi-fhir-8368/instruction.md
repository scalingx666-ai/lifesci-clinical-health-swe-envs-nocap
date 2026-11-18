# Issue

**Title:** Update bom for missing deps and correct one failure

## Description

This brings the BOM up to date with our projects, and fixes a failure in one (hapi-fhir-mdm does not exist)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `73f3d2534cbb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.