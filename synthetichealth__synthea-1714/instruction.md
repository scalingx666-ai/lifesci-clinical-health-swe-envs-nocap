# Issue

**Title:** Fix unset end timestamps in CSV exports

## Description

## Summary

This fixes CSV export behavior when an internal stop time is unset (`0L`).

Previously, the following fields could be serialized as the Unix epoch (`1970-01-01T00:00:00Z`) when their internal stop time was unset:

- `claims_transactions.TODATE`
- `payer_transitions.END_DATE`

The exporter now leaves those end-date fields empty when the stop time is unset, consistent with existing handling of unset stop times elsewhere in `CSVExporter`.

## Changes

- Guard `payer_transitions.END_DATE` against an unset plan stop time.
- Guard `claims_transactions.TODATE` against an unset claim-entry stop time.
- Add deterministic regression tests for both cases.

## Testing

Validated with:

- `CSVExporterTest`: 13 tests passed
- CSV exporter test suite: 15 tests passed
- Full `build check test`: 651 tests, 0 failures, 6 skipped

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e457b7c6294`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.