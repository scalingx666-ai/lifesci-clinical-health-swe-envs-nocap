# Issue

**Title:** Refactor CSVExporter

## Description

This branch refactors the `CSVExporter` so that it will be able to more easily be modified to support splitting the output into multiple CSV files (#1367).

The code which handles files is extracted into `CSVFileManager` so that all necessary file renaming can happen there in a future PR.

Additionally, the methods to write a resource line to a CSV file had names like `patients`, `observations`, etc., and I renamed these to `exportPatient`, `exportObservation`, etc. so that their purpose is clear at a glance.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a65f56f13e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.