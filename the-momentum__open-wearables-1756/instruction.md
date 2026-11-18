# Issue

**Title:** feat(backend): store overnight HRV from the sleep series

## Description

## What does this change?

Withings now stores overnight HRV: RMSSD and SDNN readings from Sleep v2 - Get, as timestamped samples within each night. No backfill: samples appear as nights are synced.



## Why?

The readings come from the request the hypnogram walk (#1710) already makes, by asking it for `rmssd` and `sdnn_1`, so no new request is spent against the per-app quota. The sleep summary carries only two RMSSD averages and no SDNN.

HRV is in Withings' paid biomarker pack. An app on the free plan may have the fields refused rather than left out, so a refused request is retried without them and the night keeps its stages; a throttle or a lost grant is not retried, as the bare request would fail too. A null or zero reading is dropped without taking its interval's stage along.

## How did you test this?

Unit tests, full suite. On the demo account, synced through the API: every night got its stages and its readings, with no zeros and an offset on each sample. The demo account returns paid-pack metrics regardless of plan, so the free-plan behaviour is untested.

## Worth knowing

- On a free plan this adds nothing, and the docs table marks it as paid only.

## AI usage

Claude Code for reading the Withings spec, drafting the implementation and tests, and verifying against the demo account.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Withings sleep data now includes overnight RMSSD and SDNN heart rate variability readings alongside sleep-stage information.
  * HRV readings are retained even when a nightly minimum heart rate isn’t available.
* **Documentation**
  * Updated Withings data coverage to include RMSSD and SDNN, and clarified that Sleep HRV is unavailable on the free plan.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b03587b3ffb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.