# Issue

**Title:** fix(core): parse HL7 DTM offsets and fractional seconds correctly

## Description

parseHl7DateTime sliced fixed positions before removing the +/-ZZZZ suffix, so offsets on values with less than minute precision were read as minutes/seconds ("2024011509-0500" became 14:00:50). It also read fraction digits as a millisecond count (".5" became 5 ms). formatHl7DateTime did not pad milliseconds, writing 50 ms as ".50".

Strip the offset first, read the fraction as a decimal, and pad milliseconds to three digits. Add tests for each DTM precision.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6ea6a28f985`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.