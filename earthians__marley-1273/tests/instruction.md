# Issue

**Title:** fix: preserve trailing zeros in numeric observation results (backport #1258)

## Description

Issue description

Numeric results such as serum creatinine changed from  1.0` to `1  after saving or approval. The Float input removed trailing zeros, losing the entered decimal precision.

Fix applied

- Changed Numeric and Quantity inputs to Data controls to preserve values exactly as entered.
- Retained server-side numeric validation.
- Added regression coverage for 1.0, 1.2, 1.00, and 0.0 through Observation and Diagnostic Report save and approval paths<hr>This is an automatic backport of pull request #1258 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc514c87b7d3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.