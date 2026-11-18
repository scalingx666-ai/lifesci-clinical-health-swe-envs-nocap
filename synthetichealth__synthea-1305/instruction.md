# Issue

**Title:** Adjust patient residence codes.

## Description

First pass at improving the prescription drug event patient residence codes.

The decision of which residence code is selected is based on the encounter class, and sometimes patient homelessness status.

Prior to this change, something like 99.99% of the codes were `01 - home` and an exceptionally small number were `14 - homeless`.

The following table shows the results after the change, and was based on 10K synthetic patients using `--generate.providers.selection_behavior=medicare` and `-a 65-80` 

PTNT_RSDNC_CD | Display | SYNTHETIC % | REAL % | DELTA
-- | -- | -- | -- | --
01 | home | 0.873368 | 0.802164 | +0.071204
00 | not specified | 0.085420 | 0.073489 | +0.011931
04 | assisted living | 0.040491 | 0.039337 | +0.001154
13 | inpatient rehab | 0.000577 | 0.000001 | +0.000576
11 | hospice | 0.000096 | 0.000073 | +0.000024
03 | nursing | 0.000031 | 0.084936 | -0.084905
14 | homeless | 0.000017 | 0.000001 | +0.000017

The results are pretty good, except for `03 - nursing`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ca9cb95c539`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.