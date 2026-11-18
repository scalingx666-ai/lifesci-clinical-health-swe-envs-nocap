# Issue

**Title:** [INFO] Warning : dropping support for 3 iotools

## Description

## Description
Iotools `merge-tsv` , `create_subjects_visits` and `check_missing_modalities` are all tools that could entirely depend on `clinicaio`, obviously not under the command line form.

## For the future
- Integrate into `clinicaio`
- Write python scripts to match these behaviors
- Need the `clinicaio` CAPS release for one of them

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `71d014731410`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.