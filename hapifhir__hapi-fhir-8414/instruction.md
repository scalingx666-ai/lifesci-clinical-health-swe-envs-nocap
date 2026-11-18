# Issue

**Title:** [8408] Normalize DateTimes in Periods consistently for Indexing and Search

## Description

**Context:**
This PR fixes a bug introduced in  

**Reverts:**
- Revert's 7885's change to `testTimingDateRangeSearch_ordinalAndDatetimeSearchesMatch`

**Changes:**
1. Refactored out the `Period` normalization code to prevent divergence in how we normalize `Period` and `Timing.Period` for indexing.
2. Since `BaseSearchParamExtractor` populates an internal table for searching, and is not part of the `FHIR` spec, we can set the values in whatever way is optimal for searching as long as it returns the correct results. As such, instead of `null` it now uses `max` and `min` values of `DateTime` for indexing `Period`, similar to how it is done elsewhere in the class.
3. There is existing behaviour where we expect `EventDate` to limit the results for an unbounded `Period`, this is maintained. 
4. In order to correctly select the latest end for indexing, end dates are extended using `reComputeValueHighDate` which has been lifted out of `ResourceIndexedSearchParamDate` to `DateUtils`

**Follow-ups**
This fix will require reindexing all resources containing `Period`s

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8558e9ee32cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.