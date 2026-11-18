# Issue

**Title:** Add default value for exporter.encoding in code.

## Description

and #1130.

Adds default value for `exporter.encoding` in the code.

This is important for when a `synthea.properties` file does not specify a value, which causes the effected exporters to fail. This can happen with synthea-international configurations, for example.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `794345fe95d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.