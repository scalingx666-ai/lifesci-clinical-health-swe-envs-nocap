# Issue

**Title:** Fix issue where vital signs were sometimes being set to `NaN`

## Description

Synthea's simulation of height and weight under the age of 20 depends on growth charts published by CDC. The growth charts are [provided with a method](https://www.cdc.gov/growthcharts/percentile_data_files.htm) for transforming values into percentiles and vice-versa. It appears that for higher percentiles, this method can break down. 

The case that was used for testing this issue is transforming the ~99.74th percentile BMI for females at 240 months into an actual BMI value. 

This code change addresses the issue by converting any request above the 99.5th percentile to just the 99.5th percentile.

This addresses #1372.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6192ed703d85`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.