# Issue

**Title:** Various updates to BFD RIF SNF and HHA exports

## Description

Note that there are three new mapping files (available on the file share) utilized by this PR.

1. Fix a bug where all procedures would happen in one day
2. Reduce probability of various procedures during SNF stay
3. RIF revenue center codes are now mapped from procedure codes
4. Update BFD RIF SNF exporter so that claim lines without HCPCS codes are not skipped (matches real data)
5. Add mappings to SNF PPS and PDPM codes to better match real data
6. Centralize logic that determines which events map to which BFD RIF claim files

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `afb9f156f7ce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.