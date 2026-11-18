# Issue

**Title:** Make quality of life observations in the CSV export optional

## Description

The yearly QALY, DALY, and QOLS scores are calculated from a patient's disease burden after generation rather than recorded during an encounter, so the rows written for them in observations.csv have an empty ENCOUNTER column even though the data dictionary lists that column as required.

Add exporter.csv.include_quality_of_life_observations (default true, so existing output is unchanged) to control whether those rows are written, and move the export of those rows into its own method.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29a7d63ce80e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.