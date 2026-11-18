# Issue

**Title:** Implement sex-specific NHANES sampling for pediatric growth trajectories

## Description

## Summary

Implements sex-specific initial BMI sampling from NHANES data for pediatric 
growth trajectories, producing more clinically realistic synthetic patient data.

## Problem

The `PediatricGrowthTrajectory` constructor selects an initial BMI sample from 
NHANES without considering the child's sex. Since male and female children exhibit 
different BMI distributions (CDC growth charts are sex-specific), this produces 
less realistic synthetic data — particularly problematic for studies examining 
sex-specific obesity prevalence or growth patterns.

Addresses the TODO in `PediatricGrowthTrajectory.java`:
> "Make the selection sex specific"

## Solution

- Added `NHANESSample.loadDistributionBySex(int sexCode)` — filters NHANES samples 
  by sex code (1=male, 2=female per NHANES convention) and re-normalizes probabilities
- Added new constructor `PediatricGrowthTrajectory(seed, birthTime, sex)` that selects 
  from the sex-appropriate distribution
- Updated `LifecycleModule` to pass the person's gender
- Original constructor preserved with `@Deprecated` annotation for backward compatibility

## Clinical Impact

CDC growth charts are sex-specific because male and female children have measurably 
different BMI distributions at ages 2-3. Sampling from a sex-mixed pool could assign 
a female child a BMI statistically more typical of males, producing unrealistic records 
that could mislead downstream clinical analysis or EHR testing.

## Thread Safety

Sex-specific distributions are loaded once at class initialization. Each distribution 
is synchronized independently during sampling, maintaining thread safety for parallel 
patient generation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c48eac705e15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.