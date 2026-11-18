# Issue

**Title:** fix: range results being evaluated as subtraction in diagnostic reports

## Description

Issue description

When an Observation Template’s Permitted Data Type is set to Range, entering 12-15 in a Diagnostic Report displays  -3, The Range field uses a Float control, which evaluates the input as subtraction. Backend validation also rejects hyphenated range values.

Fix applied

- Changed Range to a Data control, preserving the entered value in Diagnostic Reports and Observation forms.
- Updated backend validation to accept numeric ranges.
- Prevented interval results from being treated as zero during scalar reference-band comparisons, avoiding misleading result flags.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9e204c366f6f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.