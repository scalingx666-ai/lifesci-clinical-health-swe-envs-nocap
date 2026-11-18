# Issue

**Title:** Fix export filter keeping old entries when there is an active entry of the same type

## Description

This PR addresses an issue where the export filter isn't filtering out old entries when there is a separate active entry of the same "type", ie, code. This is especially likely to happen with "Medication Review Due" from the Med Rec module, but it could also happen for any potentially-recurring entry such as Viral Sinusitis or chronic medications.

The issue is that the logic is using `record.conditionActive` which only checks whether the given code is in the "active" set, it doesn't look at the specific entry at all. The change here is to only look at dates, and the date logic can be pretty simple: "if the entry is open (stop = 0) or the stop is after the cutoff, keep the entry"

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6192ed703d85`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.