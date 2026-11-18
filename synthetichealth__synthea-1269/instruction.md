# Issue

**Title:** Fix ethnicity display in clinical notes.

## Description

Fixes hispanic ethnicity display in clinical notes.

Previously, the template improperly printed "non-hispanic" in cases even when the patient was hispanic, because the lookup was based on the weird US Core terminology code systems.

Now, the raw attribute value of "hispanic" or "nonhispanic" is printed.

Results were validated by comparing with `patients.csv` output.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8296b0b89a78`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.