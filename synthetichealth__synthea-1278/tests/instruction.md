# Issue

**Title:** BFD Exporter Updates

## Description

1. Update BFD inpatient exporter to ensure line item totals match claim totals
2. Update BFD outpatient exporter to ensure line item totals match claim totals
3. Pull common code for inpatient and outpatient exporter up in RIFExporter base class
4. Add tests for BFD HHA exporter to ensure line item totals match claim totals
5. Update BFD SNF exporter to ensure line item totals match claim totals
6. Update BFD Hospice exporter to ensure line item totals match claim totals

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a13ec2f1a0ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.